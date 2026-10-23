# 6.2.1.4    To find out the first element of a Queue

We can determine the first element in a queue without changing the first index. Once the element(s) of a queue is displayed, it will again display all the element(s) including the first element that has been returned by the FirstElement() function. Code of the function is depicted in the following example:

```
```cpp
// Program : Write the program to determine the first element in a
queue without changing the first index.

int firstelement()
{
if(first==0)
{
cout<<" queue is empty";
return 0;
}
int x=queue[first];      // Store the first element of the stack
return x;   // return the first element
}
```
```

# 6.2.2    Main function

Functions defined in the preceding sub-sections have been performing their objectives. To call them, we can make use of main function, where they can be called as illustrated in the following example.

```
```cpp
int main()
{
clrscr();
Q q1;
q1.enqueue(90);
q1.enqueue(5);
q1.enqueue(78);
q1.enqueue(35);
q1.enqueue(10);
q1.enqueue(14);
cout<<" Total number of elements "<<q1.count()<<endl;
q1.display();
cout<<"Dequeue item: "<<q1.dequeue()<<endl;
cout<<"Dequeue item: "<<q1.dequeue()<<endl;
```
```