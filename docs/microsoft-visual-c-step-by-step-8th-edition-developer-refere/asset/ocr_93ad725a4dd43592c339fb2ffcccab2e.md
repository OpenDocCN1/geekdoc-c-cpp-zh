operands).

There is one final rule that you must follow when declaring an operator: at least one of the parameters must always be of the containing type. In the preceding operator+ example for the Hour class, one of the parameters, a or b, must be an Hour object. In this example, both parameters are Hour objects. However, there could be times when you want to define additional implementations of operator+ that add, for example, an integer (a number of hours) to an Hour object—the first parameter could be Hour, and the second parameter could be the integer. This rule makes it easier for the compiler to know where to look when trying to resolve an operator invocation, and it also ensures that you can’t change the meaning of the built-in operators.

# Creating symmetric operators

In the preceding section, you saw how to declare a binary + operator to add together two instances of type Hour. The Hour structure also has a constructor that creates an Hour from an int. This means that you can add together an Hour and an int; you just have to first use the Hour constructor to convert the int to an Hour, as in the following example:

```
Hour a = ...;
int b = ...;
Hour sum = a + new Hour(b);
```

This is certainly valid code, but it is not as clear or concise as adding an Hour and an int directly, like this:

```
Hour a = ...;
int b = ...;
Hour sum = a + b;
```

To make the expression (a + b) valid, you must specify what it means to add together an Hour (a, on the left) and an int (b, on the right). In other words, you must declare a binary + operator whose first parameter is an Hour and whose second parameter is an int. The following code shows the recommended approach:

Click here to view code image

```
struct Hour
{
    public Hour(int initialValue)
    {
        this.value = initialValue;
    }
    ...
    public static Hour operator +(Hour lhs, Hour rhs)
    {
        return new Hour(lhs.value + rhs.value);
    }
```