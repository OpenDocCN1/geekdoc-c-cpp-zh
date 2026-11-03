
- 8. assign j-1 to j
  - end if
- 9. if i<j go to step 10 otherwise go to step 4
  - begin
- 10. call function to swap k[i] and k[j]
  - end if
- 11. call function to swap k[pivot] and k[j]
- 12. call function qsort(x,lowerbound,j-1)
- 13. call function qsort(x,j+1,upperbound)
  - end if
- 14. stop

The time complexity of the quick sort algorithm is

- In worst case = O(n²)
- In average case = log₂ n
- In best case = log₂ n

### Program:

```c
#include <stdio.h>
main()
{
    int x[10],i,n;
    clrscr();
    printf("enter no of elements:");
    scanf("%d",&n);
    printf("enter %d elements:",n);
    for(i=1;i<=n;i++)
    scanf("%d",&x[i]);
    quicksort(x,1,n);
    printf("sorted elements are:");
    for(i=1;i<=n;i++)
    printf("%3d",x[i]);
    getch();
}
quicksort(int x[10],int first,int last)
{
    int pivot,i,j,t;
    if(first<last)
    {
        pivot=first;
        i=first;
        j=last;
        while(i<j)
        {
            while(x[i]<=x[pivot] && i<last)
                i++;
            while(x[j]>x[pivot])
                j--;
            if(i<j)
            {
                t=x[i];
                x[i]=x[j];
                x[j]=t;
            }
        }
        t=x[pivot];
        x[pivot]=x[j];
        x[j]=t;
        quicksort(x,first,j-1);
        quicksort(x,j+1,last);
    }
}
```

### OUTPUT

```
enter no of elements:6
enter 6 elements:
23
12
45
34
21
87
sorted elements are: 12 21 23 34 45 87
```

## 7. What are the advantages and disadvantages of stack? Write a program to illustrate stack operation?

Ans: A stack is an ordered collection of items into which new items may be inserted and items may be deleted at one end, called top of the stack. A stack is also known as LIFO structure because the element which is inserted last is the first element to be deleted.

![](img/65953ea584e494f3d396b2252cb5ea53_512_0.png)

By the definition of stack, there is no upper limit on the number of items that can be kept in a stack. Pushing an element results in a larger collection of items in the stack and popping an element leads to a lesser collection of elements.

### Representation of stack:

### Advantages of stack:

- 1. To convert infix expression to postfix expression.
- 2. stack is used in recursion
- 3. Stack is used to evaluate postfix expressions.

### Disadvantages:

- 1. In LIFO, if we want to delete the first element then all the elements are to be deleted.
- 2. As insertion and deletion are done from only one end, the other end is closed.

There are two operations that are performed in the stack. They are

- 1. push(): Inserting an element into a stack is called as pushing operation
- 2. pop(): Deleting an element from the stack is called as popping operation.

The following program illustrates the operations in a stack

### Program:

```c
/* Write a 'C' program that implements stack and its operation by using the arrays */
#include <stdio.h>
#define size 4
int choice,top=0,a[size],item;
main()
{
clrscr();
while(1)
{
printf(" *** MENU ***\n 1. PUSH\n 2. POP\n 3. TRAVERSE\n 4. EXIT\n");
printf("enter your choice from menu:");
scanf("%d",&choice);
switch(choice)
{
case 1:push();
break;
case 2:pop();
break;
case 3:traverse();
break;
case 4:exit();
default:printf("wrong choice\n");
}
}
```

communication from one graph to another graph. Graph node is connected with another node called Edge. The following graph explains and shows how the network operation is performed.

![](img/65953ea584e494f3d396b2252cb5ea53_515_0.png)

(b) Spanning trees are usually represented as graphs. Hence, spanning trees are undirected trees, residing with only those edges which are sufficient to connect all the nodes with a tree. There are two important considerations regarding a spanning tree.

- 1. Each pair of nodes in the spanning trees should possess a single path.
- 2. The number of edges in the spanning tree is one less than the total number of nodes [if a tree consists of ‘n’ nodes, then the edges should be (n-1)].
- 3. Hence, any tree passing successfully through above-mentioned considerations can be termed as a spanning tree. Here are few examples of spanning trees.

![](img/65953ea584e494f3d396b2252cb5ea53_515_1.png)

There are three major concepts associated with each spanning tree. These are

- 1. depth first search spanning tree
- 2. breadth first search spanning tree
- 3. cost of spanning tree.

The spanning tree obtained by considering the depth first search mechanism is called as depth first search spanning tree. The spanning tree obtained by considering the breadth first search mechanism is called as breadth first search spanning tree. When there is a cost associated with each edge at the spanning tree, then the cost of spanning tree is nothing but the sum of costs of all the edges of the spanning tree.

Based on the cost features of spanning tree, it has been successfully applied in various studies related to electrical circuits and determining of shortest paths in the bulk routes of networks.

(c) The minimal spanning tree (MST) of a weighted graph is a spanning tree whose sum of edge weights is minimal. The minimum spanning tree describes the cheapest network to connect all of a given set of vertices.

Kruskal's algorithm for minimal spanning tree works by inserting edges in order of increasing cost (adding as edges to the tree those which connect two previously disjoint components).

The minimal spanning tree (MST) of a graph defines the cheapest subset of edges that keeps the graph in one connected component. Telephone companies are particularly interested in minimal spanning trees, because the minimal spanning tree of a set of sites defines the wiring scheme that connects the sites using as little wire as possible. It is the mother of all network design problems.

Minimal spanning trees prove important for several reasons:

- They can be computed quickly and easily, and they create a sparse subgraph that reflects a lot about the original graph.
- They provide a way to identify clusters in sets of points. Deleting the long edges from a minimal spanning tree leaves connected components that define natural clusters in the data set.
- They can be used to give approximate solutions to hard problems such as Steiner tree and travelling salesman.
- As an educational tool, minimal spanning tree algorithms provide graphic evidence that greedy algorithms can give provably optimal solutions.

### Example of minimal spanning tree

### A weighted graph G

### The minimal spanning tree from weighted graph G

![](img/65953ea584e494f3d396b2252cb5ea53_516_0.png)

![](img/65953ea584e494f3d396b2252cb5ea53_516_1.png)

Using Kruskal's Algorithm, to find the minimum cost of the tree.

### MST Problem:

Given a connected graph G=(V,E) and a weight d:E->R+, find a minimum spanning tree T.

### Kruskal's Algorithm

- 1. Set i=1 and let E0={}
- 2. Select an edge e_i of minimum value not in E_{i-1}, such that `T_i := <E_{i-1} ∪ {e_i}>` is acyclic and define `E_i = E_{i-1} ∪ {e_i}`. If no such edge exists, Let `T = <E_i>` and stop.
- 3. Replace i by i+1. Return to Step 2.

The time required by Kruskal's algorithm is O(|E|log|V|).

### (d) Tree traversal are of three types:

- 1. In-order traversal
- 2. Pre-order traversal
- 3. Post-order traversal

### In-order traversal:

In-order traversal is given by the following steps.

- 1. traverse the left sub-tree
- 2. process the root node
- 3. traverse the right sub-tree

### Algorithm for in-order traversal (recursive):

- 1. **Step 1:** check if tree is empty by verifying root pointer R. print tree empty if R=NULL
- 2. **Step 2:** print data(R).
- 3. **Step 3:** if leftptr(R)!=NULL then call in-order(leftptr(R))
- 4. **Step 4:** if rightptr(R)!= NULL then call in-order(rightptr(R))
- 5. **Step 5:** return.

![](img/65953ea584e494f3d396b2252cb5ea53_517_0.png)

So the **in-order** of the binary tree in figure above is C—B—A—E—F—D—G.

### Pre-order traversal:

Pre-order traversal is defined as follows:

- 1. process the root node
- 2. traverse the left sub-tree in pre-order
- 3. traverse the right sub-tree in pre-order

### Algorithm for pre-order traversal:

- 1. **Step 1:** check if tree is empty by verifying root pointer R; If R=NULL, then print 'tree empty'
- 2. **Step 2:** print data(R)
- 3. **Step 3:** if leftptr(R)!=NULL then call pre-order(leftptr(R))
- 4. **Step 4:** if rightptr(R)!=NULL call pre-order(rightptr(R))
- 5. **Step 5:** return

![](img/65953ea584e494f3d396b2252cb5ea53_517_1.png)
