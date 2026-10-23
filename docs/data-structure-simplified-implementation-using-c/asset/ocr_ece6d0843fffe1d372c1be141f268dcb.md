be categorized into the following types:

+   - Non-recursive
+   - Recursive

# 1.3.2 Non-Recursive

In the non-recursive algorithm, we use conditional statement(s) or the looping statement(s) in order to solve the specific problem. This approach is considered as simple and widely utilized by the developers in their coding. Debugging the recursive algorithm is simple and needs less effort.

```
To find out the sum of n numbers
int sum_array (int x [])
{
int total=0;      //initialize the total to zero
while(x[i])
{
    total=total+x[i]; //add the element with total
    i++;  //go to the next element
}
return total;
}
```

Non-recursive algorithm has less overhead relative to recursive approach that utilizes the stack to store/save it various states. However, there are number of instances where solving the problem using the non-recursive approach is complex, for instance, traversal in a tree, Tower of Hanoi, factorial etc. In such situations, applying the recursive approach makes the programmer's life simple.

# 1.3.3 Recursive Approach

A problem that is solved using non-recursive approach can also be solved with the help of recursive approach. In the recursive algorithm, function is defined in its own term. However, function comprise of a constrain in order to prevent calling to itself infinitely. For instance, consider a case to add all the elements of an array.

```
int sum (int x [], int n)// Array element sum, recursively
{
if (n==0)   // base condition
return 0;
return total=sum(x, n-1) +x[n];      //decreasing n
}
```