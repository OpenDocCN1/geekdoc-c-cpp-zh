```
{
    yield return selector(element);
}
}
```

Assuming the System.Linq namespace was imported with a using namespace directive, and given a class Customer with a Name property of type string, the Select method can be used to select the names of a list of customers:

```
List<Customer> customers = GetCustomerList();
IEnumerable<string> names = customers.Select(c => c.Name);
```

The extension method invocation (§11.7.8.3) of Select is processed by rewriting the invocation to a static method invocation:

```
IEnumerable<string> names = Enumerable.Select(customers, c => c.Name);
```

Since type arguments were not explicitly specified, type inference is used to infer the type arguments. First, the customers argument is related to the source parameter, inferring TSource to be Customer. Then, using the anonymous function type inference process described above, c is given type Customer, and the expression c.Name is related to the return type of the selector parameter, inferring TResult to be string. Thus, the invocation is equivalent to

```
Sequence.Select<Customer, string>(customers, (Customer c) => c.Name)
```

and the result is of type IEnumerable<string>.

The following example demonstrates how anonymous function type inference allows type information to "flow" between arguments in a generic method invocation. Given the method:

```
static Z F<X,Y,Z>(X value, Func<X,Y> f1, Func<Y,Z> f2)
{
    return f2(f1(value));
}
```

Type inference for the invocation:

```
double seconds = F("1:15:30", s => TimeSpan.Parse(s), t => t.TotalSeconds);
```

proceeds as follows: First, the argument "1:15:30" is related to the value parameter, inferring X to be string. Then, the parameter of the first anonymous function, s, is given the inferred type string, and the expression TimeSpan.Parse(s) is related to the return type of f1, inferring Y to be System.TimeSpan. Finally, the parameter of the second anonymous function, t, is given the inferred type System.TimeSpan, and the expression t.TotalSeconds is related to the return type of f2, inferring Z to be double. Thus, the result of the invocation is of type double.

end example

# 11.6.3.14 Type inference for conversion of method groups

Similar to calls of generic methods, type inference shall also be applied when a method group M containing a generic method is converted to a given delegate type D (§10.8). Given a method

```
T_e M<X1...Xv>(T1 x1 ... T_e x_e)
```

and the method group M being assigned to the delegate type D the task of type inference is to find type arguments S1...Sv so that the expression:

```
M<S1...Sv>
```