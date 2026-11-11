# 10.4  delete Keyword in C++

The keyword `delete` is used to free the memory that is allocated dynamically. It is always
a good programming practice free up the resources that are occupied by the program before
the execution of the code completes. This helps in optimum utilization of the available
heap space. The following is the syntax of using `delete` keyword:

```
delete <pointer>;
```

When a keyword `delete` is followed by the name of the pointer, system will free up the
memory pointed by the pointer.

For example, let us create an integer memory of 2 bytes dynamically and store its
address in a pointer p, which can be done by using the following statement:

```
int *p=new int;
```

After performing the operations with the memory, we can free the memory pointed by the
pointer p by using the following statement:

```
delete p;
```

If the pointer p points to an array that is created dynamically then the delete statement to
free the complete array space pointed by the pointer must be written as below:

```
delete [] p;
```

# Error Finding Exercise

Given below are some programs which may or may not contain errors. Correct the error(s)
if exist in the code and determine the output.

# Program 1

```
#include<iostream.h>
void display(int *p=new int[5])
{
for(int i=0;i<5;i++)
    {
    cout<<*(p+i)<<endl;
    }
}
void main()
{
int a[]={10,20,30,40,50};
cout<<"The array elements are"<<endl;
display(a);
}
```