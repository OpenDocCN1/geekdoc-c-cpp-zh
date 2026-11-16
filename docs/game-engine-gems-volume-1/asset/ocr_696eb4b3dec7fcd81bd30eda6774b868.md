# 24.2 Using the KVD

As mentioned in the introduction, the KVD is designed to be used with general game state data that is read often, but changed relatively infrequently. Traditionally, game state data is repeatedly polled by lots of different systems. For example, the current screen resolution is a piece of data that changes very infrequently, but which is polled by a number of different systems. If you use the KVD to store the screen resolution, you don't need to poll for its value each frame, but you are instead told when the value changes and what the new value is.

Using an intermediary data store like the KVD can help decouple your classes and reduce header file dependencies. As in the previous example, if you were to store the current screen resolution inside the rendering system, every piece of code which is required to read or set this value needs to include the header file for the rendering system, and that could itself pull in other headers as illustrated in Figure 24.1, increasing compile times.

![](bbox=[0.172, 0.55, 0.59, 0.775])

Figure 24.1: A polling model for accessing information often creates additional header dependencies.

Pulling the screen resolution out of the rendering system and into an intermediary would stop your game code from having to include