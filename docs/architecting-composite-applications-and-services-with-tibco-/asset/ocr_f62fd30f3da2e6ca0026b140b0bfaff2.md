these designs, the front-end systems contained two types of logic: interface logic and business logic. The interface logic dealt with the interactions of users or other systems that required access to the back-end systems. The business logic mapped these interactions to the back-end system interfaces, deciding when such interactions were appropriate and coordinating multiple interactions when required.

The disadvantage of this approach is that adding a new type of front-end interface (e.g., a new channel for providing business services) required not only implementing the new interface but also replicating the business logic. This not only drove up the cost of adding new channels for doing business, it significantly increased the cost of evolving the business logic.

# Design Pattern: Separate Interface and Business Logic

Evolving to a service-oriented architecture affords the opportunity to refactor and separate the business logic from the interface logic (Figure 10-2). When done with an eye toward the different types of front-end systems, this would make it possible to have a single business logic implementation support more than one interface.

Consider the online banking example of Figure 10-3. Here the application server (the front-end system) guides the bank customer through the process of transferring funds between accounts. It also contains the business logic that coordinates the two interactions with back-end systems and provides the required transactional behavior.

![](bbox=[0.217, 0.654, 0.688, 0.886])

**Figure 10-2:** _Separating Interface and Business Logic_