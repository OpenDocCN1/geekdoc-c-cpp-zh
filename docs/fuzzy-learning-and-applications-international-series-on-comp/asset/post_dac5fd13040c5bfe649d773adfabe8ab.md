
## 3 Fuzzy Modeling in a Multi-Agent Framework for Learning in Autonomous Systems

Juan A. Botía

Humberto Martínez Barberá

Antonio F. Gómez Skármeta

Dep. Informática, Inteligencia Artificial and Electrónica - Facultad de Informática - Universidad de Murcia, E-30001 Murcia, Spain

- Abstract ................................................... 94
- 3.1 Introduction ............................................ 94
- 3.2 Fuzzy Modeling and Agents ............................... 95
  - Distributed Artificial Intelligence (DAI)
  - Tasks in MAS Development
  - An Agent-oriented Methodology
  - MAST. The Multi-agent System Toolbox
  - The MIX Agent model
  - MAST: the Tool for Developing Multi-Agent Systems
  - Exchanging Information Objects with MAST
- 3.3 A MAS Architecture for Fuzzy Modeling (MASAM) ............ 101
  - Agents Architecture
  - Fuzzy Modeling in our MAS Architecture
  - Fuzzy Clustering: a Central Component for Fuzzy Modeling
- 3.4 Clustering Agents ....................................... 109
  - Fuzzy LVQ
  - Fuzzy Tabu Clustering
  - Rule Generation Agents
  - A Genetic Algorithm Based Method to Generate and/or Tune Fuzzy Rules
- 3.5 Robotics Application Example ............................ 117
  - Introduction
  - The BG programming language
  - Robot agents architecture
  - Learning behaviour fusion
  - Experimental results
- 3.6 Conclusions and Future Work ............................ 133
- 3.7 References .............................................. 141

### 3.1 Introduction

...is the approach taken by hybrid systems. Over the past few years we have seen an increasing number of hybrid algorithms, in which two or more soft computing technologies have been integrated to improve the overall algorithm performance [11].

Those hybrid systems are composed of several different and interchangeable techniques. The best combination of such techniques may vary from problem to problem. This leads us to the idea of a multiple loosely coupled co-processing distributed system. Each technique can be developed as a system component and encapsulated to offer a homogeneous interface in a distributed environment. Mechanisms apt for intelligent cooperation among these components (agents) should be supported to allow the design and implementation of cooperative distributed applications.

In this chapter we propose the use of intelligent agents which collaborate by means of a multiagent architecture, as a framework to investigate different learning techniques in a fuzzy modeling context. This approach involving agents, which embody the different problem solving methods, is a potentially useful strategy for enhancing the power of fuzzy modeling systems. Our objective is to show how this framework lets us experiment with different techniques in order to select the combination that better approximated the system behavior.

### 3.2 Fuzzy Modeling and Agents

In recent times, several different techniques, which may be subsumed in the frame of Soft-computing, have appeared in the literature related with fuzzy modeling. Thus we find proposals that include fuzzy neural networks [58], and fuzzy subset theory combined with descent gradient techniques [62], or with clustering techniques [63, 62, 8], etc. Recently combinations of those techniques have been used to try to solve different problems related with systems modeling [60, 55].

Fuzzy modeling is an approach used to form a fuzzy systems model. In fuzzy modeling, the most important problem is the identification method of a system. The identification of a fuzzy model using input-output data such as the ones we are concerned with consists of two aspects: structure identification and parameter identification [54]. Fuzzy modeling is based on the idea of finding a set of local input-output relations describing a process. So it is expected that the method of fuzzy modeling can express a nonlinear process better than an ordinary method. A fuzzy model consists of a number of fuzzy if-then rules. There are two parts in a fuzzy rule: the premise and the consequent part. These parts are formed by the combination of fuzzy sets defined in the different domains of the variables. Each input-output relation is described by a fuzzy rule. The fuzzy rules are formed by partitioning, in a fuzzy way, the

#### 3.2.1 Distributed Artificial Intelligence (DAI)

DAI has been configured as a term to reference all systems that show some kind of collective behaviour of particular entities to reach a common and global goal. Those particular entities are the so-called agents. Following [46], we can say that there are three different approaches, corresponding to three different periods of research in AI (Artificial Intelligence), to look at DAI:

- Classic DAI, centered in the collective behaviour rather than in the individual one and understanding that the society formed by particular agents is more important than those individually considered;
- Autonomous DAI, focused in the individual study of agents, but taking into account that they are in a social world, and
- Commercial DAI, centered in the application of classic and autonomous DAI to practical problems of the real world.

Following the classical approach, research has been divided in the following two groups:

- **Distributed Problem Solving** (DPS) tries to solve particular problems using distributed modules (or nodes), and shared knowledge representing the problem.
- **Multi-agent Systems** (MAS) studies the coordination of the behaviours between intelligent and autonomous agents.

The main difference between the two groups is that DPSs are designed taking into account the particular problem from the beginning; so they are, in a sense, *ad hoc* solutions. Indeed, there is often a central coordinator and a preliminary established plan. However, MAS are very general mechanisms that present more autonomy in their particular members and the control is decentralized.

Nowadays, MAS have taken almost all attention among DAI researchers; so DPSs will not be mentioned anymore in this work. Instead, the study will be focused on MAS.

#### 3.2.2 Tasks in MAS Development

The following typical tasks (or problems) have to be undertaken in the development of a MAS:

1. Formulation, description, decomposition and assignation of problems for a group of agents, in order to reach the desired results,
2. Design of communication protocols to give the agents the capability to communicate and them to cooperate,
3. Design of control mechanisms to avoid that agents make decisions or actions that are not compatible or suitable with the common goal of the overall system,
4. To make the agents capable of representing and reasoning about actions and the state of other agents in the system,
5. How to detect and resolve conflicts between different points of view in the society of agents, and
6. The use of software engineering techniques to develop the MAS as the software system that it actually should be.

All points mentioned above are critical in the implementation process. However, the last point is very important in order to achieve a suitable software system.

In this engineering process, using an agent-oriented methodology is a necessary requirement, as building a MAS system is not a trivial task. In section 3.2.3, issues related with agent-oriented methodologies are discussed. Moreover, in the implementation phase of this task, work can be started from scratch, building all necessary software needed to implement the designed agents, although this implies an enormous work to be done. Instead, a MAS platform, or toolkit, can be used for this task. This type of platform is composed of a set of software tools to help in the design and implementation of multi-agent systems. This point will be detailed in section 3.2.4.

#### 3.2.3 An Agent-oriented Methodology

There are two main approaches in engineering methodologies to develop a MAS [35]. Each approach is determined by a particular main stream of influence on the basic concepts framework. The first group comes from extending object oriented methodologies and the second comes from the starting point of knowledge engineering techniques. The particular case in our work has been to use MAS-CommonKADS [35] as a methodology to develop MAS and MAST (Multi-agent Systems Tool) [30] as a software tool to build the whole system. This methodology extends CommonKADS [49], that is a knowledge engineering methodology. MAS are, in a sense, knowledge based systems; so it seems natural to build a MAS methodology over it. Developing a system using MAS-CommonKADS is based on the description of the following models:

- Agent Model: describe the agents, in the terms of reasoning capabilities, skills, services, goals, etc.
- Task Model: describe the global task of the problem, its decomposition into subtasks and the correspondence between particular tasks and agents carrying out them.
- Expertise Model: this model focuses on the knowledge based part of the problem. It follows the KADS approach that differentiates four types of knowledge: domain, task, inference and problem solving.
