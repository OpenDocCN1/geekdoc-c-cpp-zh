![](bbox=[0.27, 0.105, 0.83, 0.18])

8. As the stack is not empty, `vertex = pop();` we get 8, which is not visited. Hence, `V = {1, 2, 3, 6, 5, 7, 8}`. Push all the adjacent vertices of 8 onto the stack.

![](bbox=[0.24, 0.26, 0.86, 0.33])

9. As the stack is not empty, `vertex = pop() = 7`, which is visited; `vertex = pop() = 9`, which is not visited. Hence, `V = {1, 2, 3, 6, 5, 7, 8, 9}`. Push all the adjacent vertices of 9 onto the stack.

![](bbox=[0.27, 0.42, 0.83, 0.49])

10. As the stack is not empty, `vertex = pop() = 8`, which is visited; so again `vertex = pop() = 4`, which is not visited. Hence, `V = {1, 2, 3, 6, 5, 7, 8, 9, 4}`. Push all the adjacent vertices of 4 onto the stack.

![](bbox=[0.27, 0.58, 0.83, 0.65])

11. The stack is not empty. So the following operations yield:

```
vertex = pop() we get 7, visited
vertex = pop() we get 1, visited
vertex = pop() we get 5, visited
vertex = pop() we get 1, visited
vertex = pop() we get 2, visited
vertex = pop() we get 1, visited
vertex = pop() we get 5, visited
vertex = pop() we get 4, visited
```

12. The stack is now empty. Hence, we stop.
The set `V = {1, 2, 3, 6, 5, 7, 8, 9, 4}` represents the order in which they are visited.
Hence, the DFS of the graph (Fig. 8.13) gives the sequence as 1, 2, 3, 6, 5, 7, 8, 9, and 4.
This is shown in Fig. 8.14.