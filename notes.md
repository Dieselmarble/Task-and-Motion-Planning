#### [Sequence-Based Plan Feasibility Prediction for Efficient Task and Motion Planning](https://arxiv.org/pdf/2211.01576.pdf)

**Achivements**

Proposed PIGINet (a transformer-based architecture) that predicts the feasibility by tokenizing the plan skeleton, goal condition, and initial state as a sequence. The method can be generalize zero-shot to problems with varying object geometry.

**Motivation**

Robots planning long-horizon behavior in complex environments must be able to quickly reason about the impact of the environment’s geometry on what plans are feasible. This problem is severe when the robot configuration space is disconnected (e.g. the robot need to rearrange obstacles to pass through). This article proposed a neural net that can speed up TAMP by sorting plan skeletons by the learner’s predicted likelihoods of feasibility.

**Methodology**

Differs from prior work, which consider  only the initial and goal state instead of candidate plans. This method considers full plans all at once, allowing it to account for parameters that persist over time in other states and actions. In mathematical formulation, $$f(\mathcal{I},\pi,G) \rightarrow [0,1]$$, where $\mathcal{I}$ is inital state, $\pi$ is plan skeleton, $G$ is goal conditions. The feasibility predictor is embedded with a PDDLStream algorithm.

**Limitations**

The proposed methods perform worse on shorter horizon tasks, but is better on long horizon tasks.



#### [PDDLStream: Integrating Symbolic Planners and Blackbox Samplers via Optimistic Adaptive Planning](https://arxiv.org/pdf/1802.08705.pdf)

**Achivements**

Extend PDDL to support a generic, declarative specification for sampling feasible motion planning coefficients, and treat the procedure as black boxes. This enables the algorithm to greedily search the space of parameter bindings to more quickly solve tightly-constrained problems as well as locally optimize to produce low-cost solutions.

**Motivation**

Special purpose procedure for evaluating and producing satisfying values for low-level constraints are unknown. TAMP for complex robot (e.g. a 11 DOF arm) is time consuming. Exising methods (i.e. numerical planning) cannot handle enormous collision constraints or 3D articulated robots. Semantic attachments limits the applicability to domains that are prediscretized and finite. However, in real world we don't have access to the static facts in a discretized state space. 

**Important Concepts**

Procedural and declarative component. PDDLStream uses *streams* as an interface for incorporating sampling procedures in PDDL. Streams have both a *procedural* and *declarative* component. 

> The *procedure* component genreate a possibly infinite sequence of output values from input values. In detail, is is a conditional generator, conidtional Generator* a function from input values to a possibly infinite sequence of output values. Conditional generators construct new values that depend on existing values (e.g. robot configurations that satisfy a kinematic constraint)

> The *declarative* component specifies the **facts** that these input and output values satisfy. PDDLStream is able to model domains with infinitely-many action instances. In order to reduce a potentially infinitely-large PDDLStream problem to a sequence of finite PDDL problems. The paper introduces the *level* of a fact, a level relates to the number of stream evaluations that are required to certify a fact.

Primage:

> The *preimage* of a consistent plan $\pi$ is the set of facts that must hold to make $\pi$ executable.

$$\text{PREIMAGE}(\pi) = \bigcup_{i=1}^k \bigg(\text{pre}(a_i(\bar{x}_i)) - \bigcup_{j-i} \text{eff}(a_j(\bar{x}_j))\bigg)$$

$$U_{1<2}$$

**Methodology**

- What is PDDLStream problems and how is it described?

In order to enable easy use for AI practitioners, PDDLStream adheres to the PDDL standard when possible and adapts PDDL style and syntax when describing streams. The declarative components of PDDLStream are still described in PDDL. Actions and derived predicates are listed using a standard domain.pddl text file. The input parameters (:inp), domain facts (:dom), output parameters (:out), and certified facts (:cert) of each stream are specified in a stream.pddl text file.

- Limitations

To ensure PDDLStream is Turing-recognizable, we require that stream-certified predicates are never negated within action preconditions. The set of streams S augments the initial state I, recursively defining a potentially infinite set of facts that hold initially and cannot be changed.


