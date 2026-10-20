```
Console.WriteLine("Radius: {0}, Area: {1}", r, areaCircle);
Console.ReadLine();
}
}
}
```

After compiling and executing the code shown above, the result produced is given below.

Enter Radius:

3

Radius: 3, Area: 28.27431

# Discover Nullables

There is a special data type in C# known as nullable types. It is not just the normal range of values that can be assigned to these datatypes but also null values.

As a example, a Nullable< Int32> variable can have any value in the range of -2,147,483,648 to 2,147,483,647 or it can have a null value. In the same way, a Nullable<bool> variable can have false, true or null as its value. The syntax for the declaration of a nullable type is given below.

```
< data_type> ? <variable_name> = null;
```