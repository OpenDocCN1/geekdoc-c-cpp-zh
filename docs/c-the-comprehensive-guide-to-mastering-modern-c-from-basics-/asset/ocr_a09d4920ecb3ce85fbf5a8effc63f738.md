# 29.8 Coroutines

Coroutines are a way to run multiple functions quasi-parallel within a thread. A caller interrupts its current work by starting a coroutine. The coroutine then runs until it interrupts itself—cooperatively. The coroutine can produce an intermediate result and pass it to the caller. Later, the caller can decide that the coroutine should continue its work. And so it can go back and forth.

![](bbox=[0.256, 0.396, 0.743, 0.565])

**Figure 29.1** Functions only return; coroutines pause and resume.

There are various application patterns for coroutines. For example, you can implement a generator. The coroutine continuously generates values while the caller retrieves the values. But communication between different parts of the program is also possible. These are sometimes called channels. The same coroutine can also be controlled by multiple threads.

C++20 only provides the framework for dealing with coroutines. To actually use them, you currently have to implement the infrastructure yourself, with one