But before it could ever be optimized, its operating goals need to be properly defined. These goals and their implementations will always be game specific but are still built upon a common underlying framework of ideas. These include:

+   - Being an entry point for all players
+   - Serving as the first line of defense
+   - Performing sanity and error checking
+   - Managing and balancing bandwidth usage
+   - Ensuring proper routing of game information
+   - Providing the fastest response times possible

The frontend service acts as a middleman between the clients and the game's backend. It concentrates data from all the backend services into a single filtered usable stream for all its connected players, and vice versa. By using game specific knowledge, the frontend service can provide faster player response times while saving the backend from unwarranted traffic. Creating flow charts and use cases can greatly help target, study, and develop these potential optimizations (See Figure 6.1.3).

One possible optimization is with the addition of a local spatial database. This database can merely be a sphere tree [Ratcliff01] that holds positions, state data, and static statistical information. Since this database can end up holding data on all the players, items, and NPCs that are currently active in the game, it is best to keep this information as simple as possible. When designed right, the spatial database will take up very few resources and allow the frontend service to do more optimal work. The reason for this database and the local caching of this amount information is to allow for a quick out. If the system never has to go beyond the frontend service to provide a client with information, it never will. Also, when a player performs an action, it can be quickly perceived by everyone else connected to that same frontend service, while it is still being propagated through the rest of the system. Performing sanity checking and keeping communications to a need-to-know basis can prevent the backend from being flooded and overworked. This is true in the case of all services; once these guidelines have been implemented, there are subsequent methods to further guarantee quality and stability.

# Increasing and Upgrading Servers

When talking about increasing or upgrading servers, we primarily concern ourselves with dealing with the machines upon which the frontend services are run. The number of players supported by a distributed services system is directly proportional to the number and power of these frontend services. The system is designed in such a way that more players can be supported just by adding more frontend services, without ever having to touch the backend. This by no means suggests that the backend will never have to be changed. As a game matures and evolves, it may need more services to accomplish its goals, and thus need additional and more powerful servers to be able to reach this.