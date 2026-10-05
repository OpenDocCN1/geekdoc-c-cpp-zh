# 548 Appendix B Solutions to Exercises

Sorting two lists of numbers takes only one longer than sorting a single list.

2. Suppose the shared route length is 100, and process A has a new route with a total length of 80. It reads the shared value and enters its If Then block. process B compares the shared value to its new route length of 70, and it also enters its If Then block, and it acquires the mutex. Process B saves its solution, along with the new route length of 70, and releases the mutex. Process A acquires the mutex and saves its solution with the total route length 80.

In this case, the solution saved by process A is worse than the one saved by process B. The route length saved by process A matches a little better than the original race condition example, but the best solution is still overwritten. Process B has a local copy of what it thinks is the best route, 70, so it would not report a new solution with a route length of 70 if it found one.

Process A can save itself if it checks the shared route length after it acquires the mutex, but by adding extra step if you acquire the mutex first, there may actually be a benefit of checking the value twice.

Acquiring a mutex can be a relatively slow operation, at least compared to checking a memory location. If process A's value isn't as good as the value already stored in the shared variable, process A can learn quickly and not both acquiring the mutex.

3. B-33 shows the situation for four philosophers. Forks with a line they are dirty. The image on the left shows the initial situation, in which philosopher 4 has no forks, philosopher 1 has two forks, and the other philosophers hold their forks.

![](bbox=[0.133, 0.563, 0.796, 0.75])

**Figure B-33: In the Chandy/Misra solution with synchronized philosophers, philosopher 1 eats first, and philosopher N eats second.

When the philosophers all try to eat at the same time, philosopher 1 already has two forks, so he succeeds and is the first to eat. The others (except for philosopher 4) already hold dirty left forks, so they request right forks. Philosopher N has no forks, so he requests both forks. Because all the forks are dirty, those who have