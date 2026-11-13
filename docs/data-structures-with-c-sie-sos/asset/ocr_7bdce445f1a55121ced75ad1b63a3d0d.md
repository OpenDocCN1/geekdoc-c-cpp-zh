```
{
    int x[15];
    for(int i = 0;i<15;i++)
    {
    x[i]=i;
    }
    printarray(x);
}
void printarray(int x[])
{
    for(int i = 0;i<15;i++)
    {
    printf("Value in the array %d\n",x[i]);
    }
}
void printdetail(int x[])
{
    for(int i = 0;i<15;i++)
    {
    printf("Value in the array %d and address is %16lu\n",x[i],&x[i]);
    }
}
}
```

In the above program, the function ‘printarray’ is used to print values of each element in the array ‘aray’. To print the value and address of all the elements and its address the printdetail function is used.

Now that we know all the elements are integer type, the difference between address is 2.

All the elements in the array are placed in consecutive memory spaces. The memory addresses can be printed using place holders %16lu or %p.

Remark: A collection A of data elements is said to be indexed if any element of A, which we shall call A<sub>K</sub>, can be located and processed in a time that is independent of K. The above discussion indicates that linear arrays can be indexed. This is very important property of linear arrays. In fact, linked lists, which are covered in the next chapter, do not have this property.

# 4.5 TRAVERSING LINEAR ARRAYS

Let A be a collection of data elements stored in the memory of the computer. Suppose we want to print the contents of each element of A or suppose we want to count the number of elements of A with a given property. This can be accomplished by traversing A, that is, by accessing and processing (frequently called visiting) each element of A exactly once.

The following algorithm traverses a linear array LA. The simplicity of the algorithm comes from the fact that LA is a linear structure. Other linear structures, such as linked lists, can also be easily traversed. On the other hand, the traversal of nonlinear structures, such as trees and graphs, is considerably more complicated.