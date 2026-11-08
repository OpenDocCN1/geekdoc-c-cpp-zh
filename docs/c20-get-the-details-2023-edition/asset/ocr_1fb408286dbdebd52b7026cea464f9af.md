![](bbox=[0.26, 0.11, 0.74, 0.59])

Multiple time synchronization with an atomic bool

On average, the execution time is 0.38 seconds.

From the readability perspective, this implementation based on std::atomic is straightforward to understand. This observation also holds for the next implementation of the ping-pong game based on semaphores.

# ### 7.5.4 Semaphores

Semaphores promise to be faster than condition variables. Let’s see if this is true.