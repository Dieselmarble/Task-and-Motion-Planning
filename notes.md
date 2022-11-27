#### [Sequence-Based Plan Feasibility Prediction for Efficient Task and Motion Planning]((https://arxiv.org/pdf/2211.01576.pdf))

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

**Methodology**

PDDLStream uses *streams* as an interface for incorporating sampling procedures in PDDL. Streams have both a *procedural* and *declarative* component. The *procedure* component genreate a possibly infinite sequence of output values from input values. The *declarative* component specifies the facts that these input and output values satisfy. PDDLStream is able to model domains with infinitely-many action instances.n order to reduce a potentially infinitely-large PDDLStream problem to a sequence of finite PDDL problems. The paper introduces the *level* of a fact, a level relates to the number of stream evaluations that are required to certify a fact.
