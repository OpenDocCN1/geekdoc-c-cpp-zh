```
void show()
{
    cout << "data = " << data << endl;
}
};

void main()
{
    clrscr();
    demo d1(300);
    demo d2 = d1;
    demo d3 = copy(d1);
    d1.show();
    d2.show();
    d3.show();
    getch();
}

OUTPUT :
Copy constructor is called
Copy constructor is called
Default constructor is called
Copy constructor is called
data = 300
data = 300
data = 300
```

# EXPLANATION :

In the program we have written a copy constructor and a friend function copy. The function copy takes an object by value as argument, copies the data into another object and returned that object. In the main when demo d1 (300); executes it calls the one argument constructor and sets data for object d1 = 200. When demo d2 = d1; executes copy constructor is called and data for d2 is equal to data for d1. Now the important thing to understand. When demo d3 = copy (d1); executes, copy constructor is called as we have written demo d3 =. As we are passing d1 by value in the function copy, copy constructor will be called. Inside the function copy temporary object (temp) is created which is called default constructor and in the end we have written the object temp by value, copy constructor is called again.

If I do a small change as that instead of writing demo d3 = copy (d1); we write as :

```
demo d3;
d3 = copy(d1);
```