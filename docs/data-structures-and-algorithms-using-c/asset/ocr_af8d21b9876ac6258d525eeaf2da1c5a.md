# Depth FirstTraversal in C

We shall not see the implementation of Depth First Traversal (or Depth First Search) in C programming language. For our reference purpose, we shall follow our example and take this as our graph model –

![](bbox=[0.05, 0.16, 0.45, 0.33])

# Implementation in C

```
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

#define MAX 5

struct Vertex {
   char label;
   bool visited;
};

//stack variables
int stack[MAX]; int top = -1;

//graph variables
//array of vertices
struct Vertex* lstVertices[MAX];

//adjacency matrix
int adjMatrix[MAX][MAX];

//vertex count
int vertexCount = 0;

//stack functions
void push(int item) { stack[++top] = item;
}

int pop() {
return stack[top--];
}

int peek() {
return stack[top];
}
```