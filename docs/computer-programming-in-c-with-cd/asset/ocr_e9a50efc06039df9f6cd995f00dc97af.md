```
```cpp
tax=5*cars_p;
}
void display()
{
    cout<<"\n Number of cars who paid tax"<<cars_p;
    cout<<"\n Tax collected "<<tax;
    cout<<"\n Number of cars who didn't paid tax "<<cars_np;
}
void main()
{
    count();
    cal();
    display();
}

Output:

Enter p if car paid the tax and n if it didn't paid the tax
p
Are there more cars [y/n]
y
Enter p if car paid the tax and n if it didn't paid the tax
n
Are there more cars [y/n]
y
Enter p if car paid the tax and n if it didn't paid the tax
p
Are there more cars [y/n]
n
Number of cars who paid tax=2
Tax collected =10
Number of cars who didn't paid tax =1
```
```

After discussing scope of variable, let's discuss storage classes that determine the accessibility of the variable in a program.

# 3.4 Exploring Storage Classes

The storage classes are qualifiers that are used to specify the lifetime of the variable. The lifetime of the variable relates to the portion of the program that has access to the variable. Storage class directs the compiler how you want to store the variable in memory and how you want to access variable within the program. The storage classes are represented with their respective specifiers in C++. Table 1 shows the various storage classes and their respective specifiers: