The output of Listing 1.4 will come out to be 11, as we have used an increment operator. If the operator is altered from a++ to ++a, still the output will remain the same. Then, what is the use of having two different types of increment operators? Listings 1.5 and 1.6 clarify this difference:

Listing 1.5 shows the working of the post increment operator:

# **Listing 1.5: Working of the Post Increment Operator**

```
    #include<stdio.h>

    int main()
    {
        int a=10;
        printf(" a %d ",a++);
        getch();
        return 0;
    }
```

The output of Listing 1.5 will come out to be 10 instead of 11.

Listing 1.6 shows the same code altered to a pre increment operation:

# **Listing 1.6: Working of the Pre Increment Operator**

```
    #include<stdio.h>

    int main()
    {
        int a=10;
        printf(" A %d ",++a);
        getch();
    }
```

In this case, the output becomes 11, as the post-increment operation has a lower precedence compared to the pre-increment operation. When we use the print statement along with the post increment operator, first the original value inside the variable gets displayed and later the value is incremented; therefore, we do not get the updated value. On the other hand, in the pre-increment operation, the value contained inside the variable first gets incremented by one and thereafter all the succeeding operations take place. This is why we get an updated display with a pre-increment operation. We will deal with some more examples of pre- and post-increment operations later in this chapter.

# **Decrement Operator**

The decrement operator in C is denoted by the “ – – ” sign. The basic working of a decrement operator is similar to that of an increment operator, with the difference that a decrement operator decreases the value of a variable by one. A decrement operator can also be used as a post-decrement and pre-decrement operator.

# *Expressions in C*

An expression represents a single data item, which can be a number or a character. The expression may consist of a constant, a variable, or a reference to a function. Some examples of expressions in C are as follows:

+   - a + b
+   - a = b
+   - x = y + z
+   - e == f
+   - ++count
+   - count--