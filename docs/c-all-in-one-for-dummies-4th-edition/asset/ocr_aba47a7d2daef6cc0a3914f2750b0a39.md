integers as parameters and returns an integer. Here's the prototype for the endl function:

```
```
ostream& endl(ostream& outs);
```
```

This function takes a reference to ostream and returns a reference to ostream. And here's a typedef for a pointer to this function:

```
```
typedef ostream& (*omanip)(ostream&);
```
```

This typedef defines a new type called omanip, which is a pointer to a function that takes as a parameter a reference to ostream and returns a reference to ostream. Therefore, if you have a variable of type omanip, you can set it to the address of the endl function.

For the endl manipulator to work, you need an overloaded insertion operator function that takes two parameters: first a reference to ostream (for cout) and then omanip. The second parameter must be a reference to omanip because the second item in cout << endl is of type omanip.

![](bbox=[0.184, 0.451, 0.235, 0.515])

If you're not clear on why endl is of type omanip, think about this: There's a function called endl, and to call that function, you would type its name, an opening parenthesis, some parameters, and then a closing parenthesis. But if you leave off the parentheses, you're just taking the address of the function. And the type omanip, defined earlier, is exactly that: an address to a function. But on top of being an address, the endl function's prototype matches that for the omanip type.

Here's a possibility for the header of the overloaded insertion operator:

```
```
ostream& operator<<(ostream& out, omanip func);
```
```

You can see the parameters that this function takes: First, it takes a reference to ostream and then omanip. Consequently, to implement endl, two functions are involved. Here are their headers:

```
```
ostream& endl(ostream& outs);
ostream& operator<<(ostream& out, omanip func);
```
```

When you type cout << endl, you're not calling the endl function. Instead, you're calling the operator<< function because endl by itself — without parentheses — is

# Streaming Your Own Classes