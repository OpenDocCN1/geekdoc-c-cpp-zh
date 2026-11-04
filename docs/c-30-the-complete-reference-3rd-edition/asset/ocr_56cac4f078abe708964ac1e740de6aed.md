Here is b: 10, 10, 10

Result of a + b: 11, 12, 13

Result of a + b + c: 22, 24, 26

Result of c - a: 21, 22, 23

Result of c - b: 11, 12, 13

Result of -a: -1, -2, -3

Given c = a++
c is 1, 2, 3
a is 2, 3, 4

Resetting a to 1, 2, 3

Given c = ++a
c is 2, 3, 4
a is 2, 3, 4

# Handling Operations on C# Built-in Types

For any given class and operator, an operator method can, itself, be overloaded. One of the most common reasons for this is to allow operations between a class type and other types of data, such as a built-in type. For example, once again consider the ThreeD class. To this point, you have seen how to overload the + so that it adds the coordinates of one ThreeD object to another. However, this is not the only way in which you might want to define addition for ThreeD. For example, it might be useful to add an integer value to each coordinate of a ThreeD object. Such an operation could be used to translate axes. To perform such an operation, you will need to overload + a second time, as shown here:

```
// Overload binary + for ThreeD + int.
public static ThreeD operator +(ThreeD op1, int op2)
{
    ThreeD result = new ThreeD();

    result.x = op1.x + op2;
    result.y = op1.y + op2;
    result.z = op1.z + op2;

    return result;
}
```

Notice that the second parameter is of type int. Thus, the preceding method allows an integer value to be added to each field of a ThreeD object. This is permissible because, as explained earlier, when overloading a binary operator, one of the operands must be of the same type as the class for which the operator is being overloaded. However, the other operand can be of any other type.

Here is a version of ThreeD that has two overloaded + methods: