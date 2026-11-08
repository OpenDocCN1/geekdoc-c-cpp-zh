![](bbox=[0.184, 0.111, 0.814, 0.665])

Thread synchronization with semaphores

![](bbox=[0.119, 0.715, 0.176, 0.76])

# Distilled Information

+   - Semaphores are a synchronization mechanism used to control concurrent access to a shared resource.
+   - A counting semaphore in C++20 has a counter. Acquiring the semaphore decreases the counter, and releasing the semaphore increases the counter. If a thread tries to acquire the semaphore when the counter is zero, the thread blocks until another thread increments the counter by releasing the semaphore.