exploration, agriculture, factory automation, service industries, waste management, health care, and disaster intervention. Autonomous robots can accomplish real-world tasks without being told exactly how to do it.

Researchers try to make the coupling between perception and action as direct as possible. This aim remains the distinguishing characteristic of behavior-based robotics. The proposed SRM technique attempts to address this goal in an intelligent, stigmergic manner.

# 3.6.2 Sensitive robots

A stigmergic robot action is determined by the environmental modifications caused by prior actions of other robots. Quantitative stigmergy regards stimulus as a continuous variable. The value of such a variable modulates the intensity or probability of future actions. Qualitative stigmergy [32] involves discrete stimulus. In this case the action is not modulated. Instead, the agent switches to a different action, [32].

A qualitative stigmergic mechanism suits our aims better, since robot stigmergic communication does not rely on chemical deposition. The robot communication relies on local environmental modifications that can trigger specific actions. “Micro-rules” define action-stimuli pairs for a robot. The set of all micro-rules used by a homogeneous group of stigmergic robots defines their behavioral repertoire and determines the type of structure the robots will create [32].

Within the proposed model, the term Sensitive robots refers to artificial entities with a Stigmergic Sensitivity Level (SSL), expressed by a real number in the unit interval [0, 1]. Extreme situations are:

+   • SSL = 0 indicates that the robot completely ignores stigmergic information (is a “non-stigmergic” robot);

+   • SSL = 1 means that the robot has maximum stigmergic sensitivity.

Robots with small SSL values are highly independent and can be considered environment explorers. They have the potential to autonomously discover new promising regions of the search space. Therefore, search diversification can be sustained.

Robots with high SSL values are able to intensively exploit the promising search regions already identified. In this case the robot behavior emphasizes search intensification. The SSL value can increase or decrease according to the search space topology encoded in the robot’s previous experience.

# 3.6.3 Sensitive robot metaheuristic for solving the drilling problem

The proposed Sensitive Robot Metaheuristic (SRM) can be implemented using two teams of sensitive robots. Robots of the first team have small SSL values. These sensitive-explorer robots are called small SSL-robots (sSSL) and can sustain search diversification. Robots of the second team have high SSL values. These sensitive-