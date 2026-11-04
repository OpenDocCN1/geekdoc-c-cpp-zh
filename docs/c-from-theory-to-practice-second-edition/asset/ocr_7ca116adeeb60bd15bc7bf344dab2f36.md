```
free(p);
return 0;
}
prev = p;
p = p->next;
}
return -1;
}
```

Comments: The implementation is similar to that of del_node() in C.14.13.

Before we finish this chapter, we'd like to underline how important it is to have a basic knowledge of algorithms and data structures. To become an expert programmer in any language, not only in C, you'll definitely need it. With the data structures presented in this chapter and the algorithms in Chapter 12, we tried to introduce you to these concepts and give you an idea. Because there is still a lot to learn, our suggestion is to read a book that focuses on these subjects. It'd be for your own benefit.

# Unsolved Exercises

U.14.1 Complete the following program to read an integer and a double number and display their sum. Don't use another variable.

```
int main(void)
{
    int *p1;
    double *p2;
    ...
}
```

U.14.2 Write a program that uses a pointer variable to read three integers and display the greatest. Don't use any other variable.

U.14.3 Use the two pointer variables and complete the following function to return how many products cost less than $20 and how many more than $100.

```
void find(double *arr, int size, int *und20, int *ov100);
```

Write a program that prompts the user to enter the number of the products (i.e., size) and their prices and stores them in a dynamically allocated memory (i.e., arr). Then, the program should use the function to display how many products cost less than $20 and how many more than $100.

U.14.4 Write a program that does the following:

+   a. Allocates memory to store a number of integers. The program should prompt the user to enter that number.
+   b. The program should read those integers and store them in the allocated memory.