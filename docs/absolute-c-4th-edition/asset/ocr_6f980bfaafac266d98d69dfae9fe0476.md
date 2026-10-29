trouble, although there a few cases where it can be useful. We will not discuss standal- one references any more, nor will we use them.

As you may suspect, references are used to implement the call-by-reference parame- ter mechanism. So, the concept is not completely new to this chapter, although the phrase a reference is new.

We are interested in references here because returning a reference will allow you to overload certain operators in a more natural way. Returning a reference can be viewed as something like returning a variable or, more precisely, an alias to a variable. The syn- tactic details are simple. You add an & to the return type. For example:

```
double& sampleFunction(double& variable);
```

Since a type like double& is a different type from double, you must use the & in both the function declaration and the function definition. The return expression must be something with a reference, such as a variable of the appropriate type. It cannot be an expression, such as X + 5. Although many compilers will let you do it (with unfortu- nate results), you also should not return a local variable because you would be generat- ing an alias to a variable and immediately destroying the variable. A trivial example of the function definition is

```
double& sampleFunction(double& variable)
{
    return variable;
}
```

Of course, this is a pretty useless, even troublesome, function, but it illustrates the con- cept. For example, the following code will output 99 and then 42:

```
double m = 99;
cout << sampleFunction(m) << endl;
sampleFunction(m) = 42;
cout << m << endl;
```

We will only be returning a reference when defining certain kinds of overloaded operators.

# L-VALUES AND R-VALUES

The term l-value is used for something that can appear on the left-hand side of an assignment operator. The term r-value is used for something that can appear on the right-hand side of an assignment operator.

If you want the object returned by a function to be an l-value, it must be returned by reference.