# Program 10.2

```
//PROGRAM FOR BREADTH FIRST TRAVERSAL OF A GRAPH
#include<iostream.h>
#include<conio.h>
char queue[20],g[20][20],x,delet();
int a[20][20],m,n,i,j,state[20],front=0,rear=-1;
void insert(char),bfs();
void main()
{
clrscr();
cout<<"Enter No Of Nodes Of Graph:";
cin>>n;
cout<<"Enter The Nodes Of Graph (In Alphabets).";
for(i=1;i<=n;i++)
cin>>g[i];
cout<<"Instructions\nPress 1 If Edge Exists Otherwise Press 0\n";
for(i=1;i<=n;i++)
for(j=1;j<=n;j++)
{
cout<<g[i]<<"->"<<g[j]<<":";
cin>>a[i][j];
}
cout<<"The Order Of Visiting The Nodes:";
// Make State Of Each Node To Ready
for(i=1;i<=n;i++)
state[i]=1;
state[1]=2;
insert(g[1]);
bfs();
getch();
}
void bfs()
{
x=delete();
for(i=1;i<=n;i++)
if(g[i]==x)
break;
state[i]=3;
cout<<g[i];
// Make State Of Each Traversed Node As Visisted
for(j=1;j<=n;j++)
{
if(a[i][j]==1&&state[j]==1)
{
state[j]=2;
insert(g[j]);
}
}
```