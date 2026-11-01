Q: Is there a container class from the STL that serves as a linked list?
A: Yes, the `list` class.

Q: Is the data structure used in the Game Lobby program a linked list?
A: It shares similarities to a linked list, but it is really a queue.

Q: What's a queue?
A: A data structure in which elements are removed in the same order in which they were entered. This process is often called first in, first out (FIFO).

Q: Is there a kind of container from the STL that serves as a queue?
A: Yes, the `queue` container adaptor.

# DISCUSSION QUESTIONS

+   1. What types of game entities could you create with aggregation?
+   2. Do friend functions undermine encapsulation in OOP?
+   3. What advantages does dynamic memory offer to game programs?
+   4. Why are memory leaks difficult errors to track down?
+   5. Should objects that allocate memory on the heap always be required to free it?

# EXERCISES

+   1. Improve the `Lobby` class from the Game Lobby program by writing a friend function of the `Player` class that allows a `Player` object to be sent to `cout`. Next, update the function that allows a `Lobby` object to be sent to `cout` so that it uses your new function for sending a `Player` object to `cout`.
+   2. The `Lobby::AddPlayer()` member function from the Game Lobby program is inefficient because it iterates through all of the player nodes to add a new player to the end of the line. Add an `m_pTail` pointer data member to the `Lobby` class that always points to the last player node in the line and use it to more efficiently add a player.