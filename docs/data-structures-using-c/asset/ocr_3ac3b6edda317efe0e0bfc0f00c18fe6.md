```
visited[curr->vertex - 1] = true;
}
curr = curr->next;
}
return;
}
```

Here, `add()` and `delete()` are the member functions for adding and deleting the elements from the queue, respectively. Let us consider Fig. 8.13, the graph, again for BFS. Let us traverse the graph using a non-recursive algorithm that uses a queue. Let 1 be the start vertex. Initially, the queue is empty, and the initial set of visited vertices, V = \(\phi\).

+   1. Add 1 to the queue. Mark 1 as visited. V = {1}.

![](bbox=[0.443, 0.41, 0.672, 0.492])

+   2. As the queue is not empty, vertex = delete() from queue, and we get 1. Add all the un-visited adjacent vertices of 1 to the queue. In addition, mark them as visited. Now, V = {1, 2, 5, 4}.

![](bbox=[0.443, 0.615, 0.672, 0.685])

+   3. As the queue is not empty, vertex = delete() and we get 2. Add all the adjacent, un-visited vertices of 2 to the queue and mark them as visited. Now V = {1, 2, 5, 4, 3}.

![](bbox=[0.443, 0.775, 0.672, 0.855])

+   4. As the queue is not empty, vertex = delete() from queue, and we get 5. Now, add all the adjacent, un-visited vertices adjacent to 5 to the queue and mark them as visited.