```
[] (double x)->double { return sin(x) + cos(x); };
```

=> c++11/derivative.cpp

Now that we can create function objects on the fly and are not particularly eager to bother with their types, we are glad that our derivative generator is able to deduce types. This allows us to create a function for the approximated seventh derivative of sin 2.5x + cos x in one single expression:

Click here to view code image

```
auto d7_psc_l= derive<7>(
    [](double x) { return sin(2.5*x) + cos(x); }, 0.0001);
```

Sadly, the statement is too long for a single line in a textbook but not so in a real program.

As soon as lambdas came out, many programmers were so excited about them that they implemented every function argument with a lambda—often over many lines and containing other lambdas inside. This might be an intriguing challenge for experienced programmers, but we are convinced that decomposing monstrous nested expressions into readable pieces helps everybody (including ourselves) using and maintaining our software.

# 3.8.1 Capture

C++11 In the previous section, we parameterized a lambda by simply inserting an operation. This is not very productive for a multitude of parameters, however:

Click here to view code image

```
a= fin_diff([] (double x) { return sin(2.5 * x); }, 1., 0.001);
b= fin_diff([] (double x) { return sin(3.0 * x); }, 1., 0.001);
c= fin_diff([] (double x) { return sin(3.5 * x); }, 1., 0.001);
```

Unfortunately we cannot access variables or constants from the lambda's scope like this:

Click here to view code image

```
double phi= 2.5;
auto sin_phi= [] (double x) { return sin(phi * x); }; // Error
```