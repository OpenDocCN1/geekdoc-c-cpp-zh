zone or loading. It's like loading a new map and you expect something different when it will finish loading.

From a programmer's perspective, the challenge resides mostly near the borders. When a player moves from one server to another or is exchanging items in the border area, having players managed by different servers can lead to many potential problems if not handled correctly. Another problem is the loading of visual assets as we move around between servers. It needs to be done in the background, if you don't want the player noticing.

And since we can have interactions between players, NPCs, objects, etc. that are on different servers, we have to keep an eye on the number of messages that are sent internally, server to server. Those can skyrocket in no time if care is not taken while working out the inter-server communication details. Even if today's network hardware is more than able to manage our expected LAN traffic, we have to keep in mind that we not only need to send the packets, the recipient must process them, too. Fewer data exchange between servers means less processing.

# The Implementation

A brief explanation of the different types of servers found in our seamless world:

+   - **RemoteController:** The login coordinator and the process giving the okay to the ProxyServer to start accepting client connections.
+   - **ProxyServer:** The bridge between the outside world and our server layout.
+   - **LoginServer:** Authenticates the clients.
+   - **NodeServer:** Manages a segment of the world.
+   - **WorldManager:** Distributes the world segment to the NodeServers.

From the start, you will have a minimum of three servers: ProxyServer, LoginServer, and NodeServer. Since the number of NodeServers could vary, and we don't want to manually add lines in an ini file, we will use an autoregister system. The different servers will register themselves with the ProxyServer upon starting up (well, actually it's with the WorldManager, but that will be discussed later). This strategy lets us change the number of NodeServers as often as we like without changing a single line in an ini file.

# The RemoteController, or How to Manage the Server's Startup Period

Of course, this way of doing things led us to another potential problem. When do we start to accept incoming connections? The naïve solution would be to put a wait delay on the proxy before it starts accepting connections. Although it could work, it isn't flexible and it's quite dangerous, as you don't know if everything will be booted before it goes online.