# Disadvantages of Garbage Collection

The typical disadvantages of garbage collection process include:

+   - Garbage collection consumes computing resources to decide which piece of memory must be freed. This information may already be available with the programmer.
+   - The time at which the garbage collection process will be executed is unpredictable which may lead to stalls scattered throughout a session. This is unacceptable in real-time environments, transaction processing, or in interactive programs. Although incremental, concurrent, and real-time garbage collectors solve this problem but with some the other trade-off.
+   - Some of the bugs addressed by garbage collection can have certain security implications.

# Requirements for Automatic Garbage Collection

An effective and efficient garbage collection process must have the following properties:

+   - Must identify garbage
+   - The object or variable identified as garbage must actually be garbage.
+   - Must have less overhead
+   - During garbage collection, the execution of the program is temporarily delayed. This delay must be minimum.