# 155 Dynamic Operator Resolution

In method Plus2 the meaning of the operator + will be resolved only at run-time because v has type dynamic.

```
static dynamic Plus2(dynamic v) { return v + 2; }
```

The following calls and their results show the meaning of (+) on the run-time type of v. It can mean either int plus (which overflows in this case) or long plus (which does not) or double plus string concatenation (with conversion of 2 to a string). An attempt to apply Plus2 to false would compile fine but throw RuntimeBinderException at run-time no operator + arguments of type bool and int.

```
Console.WriteLine(Plus2(int.MaxValue-1)); // -2147483648, due to int overflow
Console.WriteLine(Plus2((long)int.MaxValue-1))); // 2147483648, no long overflow
Console.WriteLine(Plus2((11.5))); // 13.5
Console.WriteLine(Plus2("Spar")); // Spar2
```

# Example 156 Dynamic Method Argument, Return Type, and Instance Tests

Method Square takes a parameter v of type dynamic. it processes according to its run-time type, and returns a result of type dynamic. If argument v has been of type Object, then many explicit casts would be needed in the operators * and + in the delegate allocation of v. With dynamic, these casts are implicit, yet they are still performed at run-time.

```
static dynamic Square(dynamic v) {
if (v is int || v is double)
    return v * v;
else if (v is String)
    return v + v;
else if (v is Func<int,int>)
    return ([Func<int,int>](x => v(v(x)));
else
}
```

# Example 157 Arrays with Element dynamic; and dynamic as Generic Type Parameter

An array may have element dynamic. this allows the array to store a mixture of values, just like an array of Objects. In addition it makes the compiler accept all operators and methods on array elements; only at run-time will these operators and methods behave. Similarly, a generic class (or struct) and a generic interface can take dynamic as the type parameter.

```
dynamic[] arr = new dynamic[] { 19, "Electric", (Func<int,int>)(n => n+2), 3.2, false };
int number = arr[0] * 5;
String string = arr[1].ToUpper();
int result = arr[2](number);
List<dynamic> list = new List<dynamic>(arr);
IEnumerable<dynamic> xs = list;
foreach (dynamic x in xs)
... 
```