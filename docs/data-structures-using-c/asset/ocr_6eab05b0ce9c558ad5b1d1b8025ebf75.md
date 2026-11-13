![](bbox=[0.396, 0.102, 0.715, 0.283])

Fig. 8.31 Shortest paths and distances

To implement this algorithm in C++, let us use an adjacency matrix implementation as it facilitates random access to all the vertices of a graph. Moreover, by storing the weights in the matrix, we can use the matrix to give weights as well as adjacencies. We shall place a special large value 9999 (to represent >>) in positions for which the corresponding edge does not exist (Program Code 8.6).

```
PROGRAM CODE 8.6

// Shortest distance using Dijkstra's algorithm

#include<iostream.h>
#include<conio.h>
#define infinite 999
class graph
{
 int Graph[20][20];
 // // Adjacency Matrix int No_of_Vertices;
 public:
 void Accept();
 void Display();
 int Calc_Shortest_Dist();
};

void graph :: Accept()
{
 int i,j;
 cout << "Enter no of vertex";
 cin >> No_of_Vertices;
 for(i = 1; i<= No_of_Vertices; i++)
 {
 for(j = 1; j<= No_of_Vertices; j++)
 {

```