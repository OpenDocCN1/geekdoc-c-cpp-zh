Calling functions with several selected arguments is easy with the operator:

```
f(a, (x < 0 ? b : c), (y < 0 ? d : e));
```

but quite clumsy with an if-statement. If you do not believe us, try it.

In most cases it is not important whether an if or a conditional expression is used. So use what feels most convenient to you.

Ancedote: An example where the choice between if and ? : makes a difference is the replace:copy operation in the Standard Template Library (STL), §4.1. It used to be implemented with the conditional operator whereas if would be more general. This “bug” remained undocumented for approximately 10 years and was only detected by an automatic analysis in Jeremy Siek’s Ph.D. thesis [38].

# 1.4.3.3 switch Statement

A switch is like a special kind of if. It provides a concise notation when different computations for different cases of an integral value are performed:

```
switch(op_code) {
case 0: z = x + y; break;
case 1: z = x - y; cout << "compute diff\n"; break;
case 2: z = x * y; break;
default: z = x / y;
}
```

A somewhat surprising behavior is that the code of the following cases is also performed unless we terminate it with break. Thus, the same operations are performed in our example for cases 2 and 3. An advanced use of switch is found in Appendix A.2.4.

# 1.4.4 Loops

# 1.4.4.1 while- and do-while-Loops

As the name suggests, a while-loop is repeated as long as a certain condition holds. Let us implement as an example the Collatz series that is defined by

| Input: x0 |
| --- |
| 1 while xi != 1 do |
| 2 xi = { 3xi-1 + 1 if xi-1 is odd |
|     xi-1 / 2 if xi-1 is even |

As long as we do not worry about overflow, this is easily implemenited with a while-loop:

```
int x = 19;
while (x != 1) {
cout << x << '\n';
```