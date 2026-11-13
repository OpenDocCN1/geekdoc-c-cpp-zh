![](bbox=[0.25, 0.1, 0.75, 0.22])

# STEP-2 While Q != $\phi$

Since Q is not empty so S = Head[Q]
for each v $\in$ Adj[u]
i.e/ for each v $\in$ Adj[S]
find Adj[S] = [R, W]
if color[v] = white i.e/ color[R] = WHITE and color[W] = white
so color[R] = gray and color[W] = gray
d[v] = d[u] + 1 i.e/ d[R] = d[S] + 1 = 0 + 1 = 1
d[W] = d[S] + 1 = 0 + 1 = 1
ENQUEUE(Q,v)
i.e/ ENQUEUE(Q,R) and ENQUEUE(Q,W)
DEQUEUE(Q) and color[S] = BLACK
So DEQUEUE(S) and color[S] = black.

![](bbox=[0.2, 0.48, 0.8, 0.62])

# STEP-3

![](bbox=[0.15, 0.645, 0.85, 0.78])

# STEP-4

![](bbox=[0.15, 0.805, 0.85, 0.95])