+   (a) 52  
+   (b) 254  
+   (c) 54  
+   (d) None of the above

+   2. We declare a pointer as (type *pointer name) where type signifies  
+   (a) Type of pointer  
+   (b) Type of data that it points to  
+   (c) Has no significance  
+   (d) Optional

+   3. The address of variable a can be obtained by using  
+   (a) &a  
+   (b) *a  
+   (c) address(a)  
+   (d) address(*a)

+   4. If a points to a string than we can access 5th character using  
+   (a) * (a+5)  
+   (b) a[5]  
+   (c) Both a and b  
+   (d) None of the above

+   5. *a++ can be taken as  
+   (a) (*a)++  
+   (b) *(a++)  
+   (c) Both a and b  
+   (d) None of the above

+   6. The general syntax of defining a pointer is  
+   (a) <data type> * <pointer name>;  
+   (b) <data type> <pointer name>;  
+   (c) <data type> &<pointer name>;  
+   (d) None of the above

+   7. & operator is known as  
+   (a) Reference operator  
+   (b) Address of operator  
+   (c) Both a and b  
+   (d) None of the above

+   8. * operator is known as  
+   (a) Value of operator  
+   (b) Multiplication operator  
+   (c) Both a and b  
+   (d) None of the above

9. The output of the following code is void

```
main()
{
    int i = 5, j = 2;
    junk(i, j);
    printf("\\n%d %d", i, j);
}

junk(int i, int j)
{
    i = i * i;
    j = j * j;
}
```

10. The output of the following code is.

```
main()
{
    int i = 5, j = 2;
    junk(&i, &j);
    printf("\\n%d %d", i, j);
}

junk(int *i, int *j)
{
    *i = *i * *i;
    *j = *j * *j;
}
```

+   (a) 52  
+   (b) 254  
+   (c) 54  
+   (d) None of the above

# State True/False

+   1. &x returns the “address of x” in hexadecimal format.  
+   2. %p is the format specifier for address.  
+   3. ‘*’ identifier acts as dereference operator can be translated to “value pointed by”.  
+   4. Base address is the address of last element of array.  
+   5. Array indexing method is faster than pointer method.  
+   6. A pointer can store a reference to a pointer.  
+   7. you cannot modify the variable by accessing it through pointers.  
+   8. A function may contain more than one return statements.  
+   9. Each return statement in a function may return a different value.  
+   10. A function can still be useful even if you do not pass any arguments to it and the function does not return any value back.

# Section B

# Short Answer Type Questions

+   A. Point out the errors, if any, in the following programs.

```
1. void main()
{
    int i = 135, a = 135, k ;
    k = pass(i, a);
    printf("\\n%d", k);
}
pass(int j, int b)
```