```
int m = 100;
object om = m; // creates a box to hold m
```

When executed, this code creates a temporary reference_type ‘box’ for the object on heap. We can also use a C-style cast for boxing.

```
int m = 100;
object om = (object)m; //C-style casting
```

Note that the boxing operation creates a copy of the value of the m integer to the object om. Now both the variables m and om exist but the value of om resides on the heap. This means that the values are independent of each other. Consider the following code:

```
int m = 10;
object om = m;
m = 20;
Console.WriteLine(m); // m = 20
Console.WriteLine(om); //om = 10
```

When a code changes the value of m, the value of om is not affected.

# 4.12.2 Unboxing

Unboxing is the process of converting the object type back to the value type. Remember that we can only unbox a variable that has previously been boxed. In contrast to boxing, unboxing is an explicit operation using C-style casting.

```
int m = 10;
object om = m; //box m
int n = (int)om; //unbox om back to an int
```

When performing unboxing, C# checks that the value type we request is actually stored in the object under conversion. Only if it is, the value is unboxed.

When unboxing a value, we have to ensure that the value type is large enough to hold the value of the object. Otherwise, the operation may result in a runtime error. For example, the code

```
int m = 500;
object om = m;
byte n = (byte)om;
```

will produce a runtime error.

Notice that when unboxing, we need to use explicit cast. This is because in the case of unboxing, an object could be cast to any type. Therefore, the cast is necessary for the compiler to verify that it is valid as per the specified value type.

# Case Study

# Problem Statement

ForEx Enterprises is a medium sized organisation that is involved in the money exchange business. This means that the main function of ForEx is to convert the money of one currency to the money of another currency for its customers. ForEx Enterprises was started in 2000 and since then it has been manually calculating the value of foreign currency into domestic currency and vice versa. Manual calculation of money value in a specific currency is recently leading to the occurrence of a large number of errors. In addition, the staff of ForEx Enterprises is spending a lot of its time in the process of converting the currency value of a certain amount of money into another currency value. How can the management of ForEx Enterprises automate the task of converting the money value of a specific currency into the money value of another currency?