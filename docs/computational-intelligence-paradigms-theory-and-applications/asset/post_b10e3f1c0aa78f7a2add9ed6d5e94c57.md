
original applications for which the algorithms were developed are different. While GAs were designed to solve discrete or integer optimization problems, ESs were applied first to continuous parameter optimization problems associated with laboratory experiments.

ESs differ from traditional optimization algorithms in some important aspects like:

- They search between populations of solutions, rather than from individual to individual.
- They use only objective function information, not derivatives.
- They use probabilistic transition rules.

The basic structure of an ES is very similar to that of a basic GA. One minor change from the standard optimization routine flow diagram is the use of the word ‘population’ rather than ‘solution’. A more major difference is that the usual operation of generating a new solution has been replaced by three separate activities — population selection, recombination, and mutation. It is in the implementation of these operations that the differences between ESs and GAs lie.

## 1.6 Swarm Intelligence

The collections of birds and animals, such as flocks, herds and schools, move in a way that appears to be orchestrated. A flock of birds moves like a well-choreographed dance troupe. They veer to the left in unison, then suddenly they may all dart to the right and swoop down toward the ground. How can they coordinate their actions so well? In 1987, Reynolds created a “boid” model, which is a distributed behavioral model, to simulate on a computer the motion of a flock of birds. Each boid is implemented as an independent actor that navigates according to its own perception of the dynamic environment. A boid must observe the following rules. First, the “avoidance rule” says that a boid must move away from boids that are too close, so as to reduce the chance of in-air collisions. Second, the “copy rule” says a boid must fly in the general direction that the flock is moving by averaging the other boids’ velocities and directions. Third, the “center rule” says that a boid should minimize exposure to the flock’s exterior by moving toward the perceived center of the flock. Flake added a fourth rule, “view”, that indicates that a boid should move laterally away from any boid that blocks its view. This boid model seems reasonable if we consider it from another point of view: that of it acting according to attraction and repulsion between neighbors in a flock. The repulsion relationship results in the avoidance of collisions and attraction makes the flock keep shape, i.e., copying movements of neighbors can be seen as a kind of attraction. The center rule plays a role in both attraction and repulsion. The swarm behavior of the simulated flock is the result of the dense interaction of the relatively simple behaviors of the individual birds.

The types of algorithms available to solve the collective behavior pattern are Particle Swarm Optimization and Ant Colony Optimization, respectively. Particle Swarm Optimization (PSO) is a swarm intelligence based algorithm to find a solution to an optimization problem in a search space, or model, and predict social behavior in the presence of objectives. The Ant Colony Optimization algorithm (ACO) is a probabilistic technique for solving computational problems which can be reduced to finding good paths through graphs. They are inspired by the behavior of ants in finding paths from the colony to food. Ant systems are also discussed further, where interaction between individuals occurs indirectly by means of modifications to the environment in which they function. By modeling these social interactions, useful algorithms have been devised for solving numerous problems including optimization and clustering.

## 1.7 Other Paradigms

Some of the major paradigms of computational intelligence are granular computing, chaos theory, and artificial immune systems. Granular computing is an emerging computing paradigm of information processing. It concerns the processing of complex information entities called information granules, which arise in the process of data abstraction and derivation of knowledge from information. Chaos theory is a developing scientific discipline, which is focused on the study of nonlinear systems.

The specific example of a relatively new CI paradigm is the Artificial Immune System (AIS), which is a computational pattern recognition technique, based on how white blood cells in the human immune system detect pathogens that do not belong to the body. Instead of building an explicit model of the available training data, AIS builds an implicit classifier that models everything else but the training data, making it suited to detecting anomalous behavior in systems. Thus, AIS is well suited for applications in anti-virus software, intrusion detection systems, and fraud detection in the financial sector.

Further, fields such as Artificial Life (ALife), robotics (especially multi-agent systems) and bioinformatics are application areas for CI techniques. Alternatively, it can be argued that those fields are a breeding ground for tomorrow’s CI ideas. For example, evolutionary computing techniques have been successfully employed in bioinformatics to decipher genetic sequences. Hand in hand with that comes a deeper understanding of the biological evolutionary process and improved evolutionary algorithms.

As another example, consider RoboCup, a project with a very ambitious goal. The challenge is to produce a team of autonomous humanoid robots that will be able to beat the human world championship team in soccer by the year 2050. This is obviously an immense undertaking that will require drawing on many disciplines. The mechanical engineering aspects are only one of the challenges standing in the way of meeting this goal. Controlling the robots is quite another. Swarm robotics, an extension of swarm intelligence into robotics, is a new paradigm in CI that may hold some of the answers. In the meantime, simulated RoboCup challenges, which are held annually, will have to suffice.

### 1.7.1 Granular Computing

Uncertainty processing paradigms can be considered as conceptual frames. Information granule is a conceptual frame of fundamental entities considered to be of importance in a problem formulation. That conceptual frame is a place where generic concepts, important for some abstraction level, processing, or transfer of results in outer environment, are formulated. Information granule can be considered as knowledge representation and knowledge processing components. Granularity level (size) of information granules is important for a problem description and for a problem-solving strategy. Soft computing can be viewed in the context of computational frame based on information granules, and referred to granular computing. Essential common features of problems are identified in granular computing, and those features are represented by granularity.

Granular computing has the ability to process information granules, and to interact with other granular or numerical world, eliciting needed granular information and giving results of granular evaluations. Granular computing enables abstract formal theories of sets, probability, fuzzy sets, rough sets, and maybe others, to be considered in the same context, noticing basic common features of those formalisms, providing one more computing level, higher from soft computing, through synergy of considered approaches. Since several computing processes can be present in the same time, with possible mutual communication, a distributed processing model can be conceived. In that model every process, or agent (Figure 1.4), is treated as a single entity.

![](img/d9a4cc12c48f7466f309cbd3c4549c73_46_0.png)

**FIGURE 1.4:** An Agent

Every agent, as shown in Figure 1.5, acts in its own granular computing environment and communicates with other agents.

![](img/d9a4cc12c48f7466f309cbd3c4549c73_46_1.png)

**FIGURE 1.5:** Granular computing implemented by agents

A formal concept of granular computing can be expressed by four-tuple <X,F,A,C>, where: X - is universe of discourse, F - is formal granulation frame, A - is a collection of generic information granules, and C - is a relevant communication mechanism. Granular computing becomes a layer of computational intelligence, a level of abstraction above soft com-
