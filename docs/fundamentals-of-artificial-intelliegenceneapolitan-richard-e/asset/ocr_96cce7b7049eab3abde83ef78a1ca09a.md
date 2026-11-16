There is gas in the fuel tank.

there is gas in the carburetor.

Rule 4 now triggers and we conclude

The engine is getting enough gas.

We now return to rule 2 and conclude that

The problem is spark plugs.

An actual production system may use both forward chaining and backward chaining in turn. That is, it could first use forward chaining to conclude all that it can based on the user’s initial knowledge. If that is not enough to make a diagnosis, it could then use goal-driven backward chaining.

In many complex diagnostic problems such as medical diagnosis, we cannot be sure of our conclusions. For example, based on a patient’s manifestations, a physician may determine that is highly probable the patient has bronchitis, less probable that the patient has lung cancer, and only slightly probable that the patient has both diseases. To develop a diagnostic system that performs this type of reasoning, we need probability theory rather than logic. Section 6.7 shows such a system.

# 2.3.2 Wumpus World

The **wumpus** world is a simple environment that has components similar to those found in many real environments. A sample wumpus world appears in Figure 2.3. The world consists of a 4-by-4 grid. An agent begins in the lower left-hand corner. The agent can move up, down, left, or right. The agent’s goal is to get to the square containing the gold, but there are dangers along the way. The only things the agent knows are its location and information it gathers as it moves from square to square. The specifics of the environment are as follows:

+   1. An evil wumpus is in one of the squares. If the agent enters that square, the wumpus will kill the agent.

+   2. There is a stench in each square adjacent to the square containing the wumpus. The agent perceives this stench if the agent enters this square.

+   3. Several of the squares contain pits. If the agent enters a square containing a pit, the agent will fall into the pit and die.

+   4. There is a breeze in any square adjacent to a pit. The agent perceives this breeze if the agent enters this square.

+   5. There is gold in one of the squares. The agent perceives the gold if the agent is in this square.