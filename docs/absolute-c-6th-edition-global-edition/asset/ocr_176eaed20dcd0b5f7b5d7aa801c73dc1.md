```
void productOut(int n1, int n2, int n3)
{
    cout << "The product of the three numbers "
         << n1 << ", " << n2 << ", and "
         << n3 << " is " << (n1*n2*n3) << endl;
}
```

18. These answers are system-dependent.

19. double sqrt(double n);
//Precondition: n >= 0.
//Returns the square root of n.

You can rewrite the second comment line as follows if you prefer, but the previous version is the usual form used for a function that returns a value:

```
//Postcondition: Returns the square root of n.
```

20. If you use a variable in a function definition, you should declare the variable in the body of the function definition.

21. Everything will be fine. The program will compile (assuming everything else is correct). The program will run (assuming that everything else is correct). The program will not generate an error message when run (assuming everything else is correct). The program will give the correct output (assuming everything else is correct).

22. The comment explains what action the function takes, including any value returned, and gives any other information that you need to know in order to use the function.

23. The principle of procedural abstraction says that a function should be written so that it can be used like a black box. This means that the programmer who uses the function need not look at the body of the function definition to see how the function works. The function declaration and accompanying comment should be all the programmer needs in order to use the function.

24. When we say that the programmer who uses a function should be able to treat the function like a black box, we mean the programmer should not need to look at the body of the function definition to see how the function works. The function declaration and accompanying comment should be all the programmer needs in order to use the function.

25. It helps to slightly change the code fragment to understand to which declaration each usage resolves. The code has three different variables named x. In the following we have renamed these three variables x1, x2, and x3. The output is given in the comments.

```
{
    int x1 = 1; // output in this column
    cout << x1 << endl; // !<new line>
    {
        cout << x1 << endl; // !<new line>
        int x2 = 2;
```