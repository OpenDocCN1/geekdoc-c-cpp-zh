# Container Access Running Times

Now we know about big-O notation, we can express the efficiency of some of the accessing functions for container classes that we discussed in Section 19.2. Insertions at the back of a vector (push_back), the front or back of a deque (push_back and push_front), and anywhere in a list (insert) are all O(1) that is, a constant bound on the running time that is independent of the size of the container. Insertion or deletion of an arbitrary element for a vector or deque is O(N) where N is the number of elements in the container. For a set or map finding, (find) is O(log N) where N is the number of elements in the container.

# Self-Test Exercises

+   18. Show that a running time T(N) = aN + b is an O(N) running time. (Hint: The only issue is the plus b. Assume N is at least 1.)
19. Show that for any two a and b for logarithms, if a and b are both greater than 1, there is a constant c such that loga N ≤ c log N. Thus, there is no need to specify a base in O(log N). That is, O(log N) and O(log N) mean the same thing.

Display 19.16 Comparison of Running Times

![](bbox=[0.235, 0.487, 0.875, 0.943])