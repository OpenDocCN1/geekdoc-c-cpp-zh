
able data. In addition, a snapshot of that shared memory can be taken every few minutes and copied to another segment of memory as a backup. Normally, this process should be very fast and take up few resources. The backing up to disk could then be done at leisure in the background from these backup segments of memory. Synchronizing these game state snapshots across the services can be done with a simple message sent to all the services. Since each service performs a specific task, and those tasks are done in small steps, they are allowed to process their current event, queue all incoming events, copy current shared memory, and then resume normal operation. Once this has taken place, the new active service can begin sending its own snapshots to other servers. This is done so that a game state backup can always be found on the network and easily retrieved when needed.

## Restoring Saved Game States

Depending on the game’s architecture, there are two methods to restoring a saved game state when a service goes down. The first method is appropriate when the game’s state requires it to be time synced; all services would then need to be reverted. The second method is used when your services are structured to be independent enough to allow only single services to be reverted.

When only one service needs to be reverted, the system finds the service server that failed, locates a server with enough spare resources to run the needed service, and then tells it to start that service up. A running server with the dead service’s most recent snapshot then pushes its snapshot to that new server, and the system instructs that service to load its previously saved snapshot.

However, in a game architecture that requires all services to be reverted on failure of a single service, the process is basically a domino effect. As before, the system locates a spare service server, has the dead service’s saved game state pushed to it, and then instructs the server to load that previously dead service in an idle state. After the service is loaded, the system takes down each individual service, has them restarted, and loads a snapshot of the same timestamp. When all services have been restarted, the system then resumes normal game operation. The restoration of the game state is based on the frequency that the snapshots are saved and sent to other servers.

## Conclusion

Online games are rapidly maturing and evolving and so are the players. Their demands and expectations will always continue to increase just as fast. As with any progress, the problems of the past will no longer be viewed as acceptable. The distributed services approach and the improvements discussed in this article are just the tools to help keep up with this pace. With all these tools in place, we can now meet the current demands of these players. In the end, size, duration, and continuity are just a few of the keys to winning their hearts.

## References

[Ratcliff01] Ratcliff, John W. "Sphere Trees for Fast Visibility Culling, Ray Tracing, and Range Searching." Game Programming Gems 2. Charles River Media, Inc., 2001

[Street05] Street, Shea. "Massively Multiplayer Games Using a Distributed Services Approach." In Massively Multiplayer Game Development 2. Charles River Media, Inc., 2005

## Implementing a Seamless World Server

Patrick Duquette, UBISOFT Entertainment Inc.
gizmo@gizz-moo.com

In [Beardsley03], the author provided an introduction to seamless world servers and their pros and cons. He did a great job of making us think of the many issues inherent with a seamless world. This article relates a journey, in the world of a too-many-times-shunned server design. It will focus on the actual implementation of a seamless world server, complete with world nodes, a proxy, and a login server. In the course of the article, we will look at the design decision normally encountered with this type of server and wrap the article with a “where to go from here” section outlining some areas for further exploration.

## The Mandatory Definition

By definition, a seamless world is a world where the player is free to roam, explore, and travel to his heart’s content. No physical barriers between “zones” to hinder your travel and no loading screen while transitioning between the zones. Designers no longer need to put mazes between zone borders in a seamless world and, having fewer constraints, they can let their imaginations run free.

Although seamless worlds can benefit any game genre since it’s the core of the server and the game specific world should reside on top of it, the immersive gains will vary depending on genres and gameplay designs. RPG games benefit from having a huge, continuous world through which the player can travel. And FPS games can now have wars that can unroll on vast expanses of terrain. Taking away the physical zones greatly boosts the player’s immersion in the game.

Of course, this level of freedom comes at a cost. The artists need to create transition areas to join different climates, just like in real life. While in traditional zoned worlds, you could have sub-tropical zones next to zones with frosty mountain ranges without disorienting the player, because you expect the hard cut between the two parts of the world and you have time to “disconnect” from the game when changing zone or loading. It's like loading a new map and you expect something different when it will finish loading.

From a programmer's perspective, the challenge resides mostly near the borders. When a player moves from one server to another or is exchanging items in the border area, having players managed by different servers can lead to many potential problems if not handled correctly. Another problem is the loading of visual assets as we move around between servers. It needs to be done in the background, if you don't want the player noticing.

And since we can have interactions between players, NPCs, objects, etc. that are on different servers, we have to keep an eye on the number of messages that are sent internally, server to server. Those can skyrocket in no time if care is not taken while working out the inter-server communication details. Even if today's network hardware is more than able to manage our expected LAN traffic, we have to keep in mind that we not only need to send the packets, the recipient must process them, too. Fewer data exchange between servers means less processing.

## The Implementation

A brief explanation of the different types of servers found in our seamless world:

- **RemoteController:** The login coordinator and the process giving the okay to the ProxyServer to start accepting client connections.
- **ProxyServer:** The bridge between the outside world and our server layout.
- **LoginServer:** Authenticates the clients.
- **NodeServer:** Manages a segment of the world.
- **WorldManager:** Distributes the world segment to the NodeServers.

From the start, you will have a minimum of three servers: ProxyServer, LoginServer, and NodeServer. Since the number of NodeServers could vary, and we don't want to manually add lines in an ini file, we will use an autoregister system. The different servers will register themselves with the ProxyServer upon starting up (well, actually it's with the WorldManager, but that will be discussed later). This strategy lets us change the number of NodeServers as often as we like without changing a single line in an ini file.

## The RemoteController, or How to Manage the Server's Startup Period

Of course, this way of doing things led us to another potential problem. When do we start to accept incoming connections? The naïve solution would be to put a wait delay on the proxy before it starts accepting connections. Although it could work, it isn't flexible and it's quite dangerous, as you don't know if everything will be booted before it goes online. The second option is to have the proxy wait on a special packet containing a “go online” command. This way you can control precisely when is the proxy server goes online. This packet will be sent only when all the conditions of the RemoteController are met. Some conditions are: making sure that the LoginServer is up, that the WorldManager has handed all the world segments to the NodeServers, etc.

The RemoteController is more than just a convenience, it is an invaluable tool to schedule the server boot up period. The alternative would be to manually control the ProxyServer, which can lead to human error and everything that comes with it.

## ProxyServer

As with many online games, you don't want to expose your server architecture to the outside world. One way to achieve that is to make all communication pass through a proxy server that will relay the packets to the right recipient. This technique has the advantage of having only one external entry point and hiding the actual servers’ layout out from the client. If you need to change your server layout, number, or internal protocol, you can do so and the client will be none the wiser, since the only thing it knows is the proxy.

This server will handle all the incoming and outgoing packets between the clients and our servers and thus handle the most traffic. With that in mind, the proxy server can be implemented using IO Completion Port (IOCP), since it doesn’t take much resource, while being able to service many concurrent clients’ connections. For a good introduction to IOCP and other relevant windows socket paradigm, please refer to [Jones02].

On a live setup, you would want to have many ProxyServers to spread the load. The client would connect to a master redirector, which will tell the client which ProxyServer to use based on current work load and latency (ping time) from the client. This will enable you to have ProxyServers distributed in the world while maintaining a single connection point for the client.

When the ProxyServer receives an incoming connection from an unknown client, it forwards it to the LoginServer for authentication. Once the credentials of the client are verified, the LoginServer notifies the ProxyServer of the client’s spawn point and NodeServer handling the spawn location.

The client connections are internally maintained via a simple array that does the translation between the ClientID and the NodeServer to which it should connect. The ClientID is the index of the array and is handed by the ProxyServer when it receives the authentication confirmation from the LoginServer. The ProxyServer allocates at boot time the array, knowing the maximum number of connections it will support. It also keeps a list of unused connections for fast management of client connections and disconnections. To minimize the possibility of a malicious user spoofing a client while it is connected, we store the connection details alongside the NodeServer to which it will connect. Once in a while, we check that the packet we received is really coming from the legitimate client.
