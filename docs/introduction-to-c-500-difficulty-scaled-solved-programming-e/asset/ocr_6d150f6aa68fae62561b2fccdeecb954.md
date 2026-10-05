```
else if (tmp > 0)
np->right = add_node(p->right, key);
else
    cout << "Error: Key " << key << " exists\n";
}
return p;
```

```
void delete_tree (Node *p)
{
    if(p == nullptr)
        return;

    delete_tree(p->left);
    delete_tree(p->right);
    cout << p->key << '\\n';
    delete p->key;
    delete p;
}
```

Before finishing this chapter, I'd like to note that although the standard library provides many ready-to-use algorithms (e.g., sort()) and containers (e.g., list) it is very to have experience in implementing algorithms and data structures. Not only because you need that knowledge to write your own applications or understand code written by others, but also to get an idea about how they are implemented. With the implementation examples of the data structures we described in this chapter and the algorithms in Chapter 12, I tried to give you this feeling of know-how. Of course, you should read a book that focuses on this subject.

# UNSOLVED EXERCISES

U.14.1 Complete the following program to read an integer and a double number and display their sum. Don't use another variable.

```
int main()
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

Write a program that prompts the user to enter the number of the products (i.c., size), their prices, and stores them in a dynamically allocated memory (i.c., arr). Then, the program should use the function to display how many products cost less than $20 and how many more than $100.