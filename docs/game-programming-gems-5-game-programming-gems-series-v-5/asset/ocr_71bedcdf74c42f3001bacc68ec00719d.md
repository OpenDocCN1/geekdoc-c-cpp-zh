# Neighbors

The NodeServer can request from the WorldManager its neighbors. This can be done at boot up or every time you need to check if you have dynamic borders (see the “Where to Go from Here” section at the end of the chapter). In the simpler “strip world” example, we can only have two neighbors. Our implementation is simplified greatly by this, and as such, we only have two member variables keeping the information associated with the neighbors. If the info is not set, we ask the WorldManager who they are and then we initiate a communication channel with them that will be kept until the server is shut down.

# The WorldManager

The WorldManager server is responsible for splitting the world into different manageable segments and giving each segment to a different NodeServer. When the manager has handed out all the world segments, it sends a message to the RemoteController, telling it that the world is distributed. This will ensure that we can’t start receiving player connection while segments of the world won’t be managed and thus inaccessible.

Subsequent connections to the WorldManager asking for a piece of the world are ignored in a Strip World implementation, as there’s no provision for backup NodeServers; this is discussed in the “Where to Go from Here” section. Also, the number of segments of the world is already known at boot time, so that when the node servers connect, they are handed a segment of the world immediately.

Another task of the WorldManager is to answer requests from the LoginServer and NodeServers as to which NodeServer handles a certain part of the world. This is vital since from one player session to another, if the server was shut down, we can’t guarantee which NodeServer will handle the part of the world from which the player disconnected. This may seem strange and inefficient, but it does free us from having to manually specify world boundaries for each NodeServer, and it makes an automated process when introducing new NodeServer in our layout, be it from expansion or because a server crashed.

# Where to Go from Here

Dynamically managing the world segments, instead of statically, is one area for improvement. If a NodeServer is overcrowded, the WorldManager could receive a request for backup processing. By resizing the borders or splitting the current world segment in two, giving the other half to a backup NodeServer would alleviate the server if the need arises. The NodeServer will have to support direct transfer of managed entities without going through the ProxyObject creation normally associated with entities crossing the NodeServers border.

Having backup NodeServers registered to take the load of a dying NodeServer could also help recover from hardware fault without interrupting the service. If a NodeServer monitors the hardware notifications, it can react to them. Instead of clos-