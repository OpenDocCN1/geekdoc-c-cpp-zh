exits to other rooms. These represent the topology of the network and cannot be changed. A room also has contents, such as the creatures who are currently in the room and things that may be acquired. The contents of a room change as creatures move around and as they carry things to and from other rooms. We will computationally model this set of named properties as a table from names to property values.

There is a set of generic procedures that are appropriate for this world. For example, some things, such as books, creatures, and the avatar, are movable. In every case, moving a thing requires deleting it from the contents of the source, adding it to the contents of the destination, and changing its location property. This operation is the same for books, people, and trolls, all of which are members of the “movable things” set.

A book can be read; person can say anything; a troll can bite a creature. To implement these behaviors there are specific properties of books that are different from the properties of people or those of trolls. But these different kinds of movable things have some properties in common, such as location. When such a thing is instantiated, it must make a table for all of its properties, including those inherited from more inclusive sets. The rules for implementing the behavior of operators as move must be to find appropriate handlers for manipulating the properties in each case.

# The game

Our game is played on a rough topological map of MIT. There are various autonomous agents (non-player characters), such as students and officials. The registrar, for example, is a troll. There are movable and immovable things, and movable things can be taken by an autonomous agent or the player's avatar. Although this game has a little detail, it can be expanded to a very interesting gjs

We create a session with an avatar named gjs who appears in a random place. The game tells the player about the environment of the avatar.

```
(start-adventure 'gjs)
You are in dorm-row
You see here: registrar
You can exit: east
```