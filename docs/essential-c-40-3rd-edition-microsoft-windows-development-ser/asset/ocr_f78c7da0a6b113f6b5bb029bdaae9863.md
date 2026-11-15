# LISTING 2.36: Assigning without Literal Values

```
string[] languages = new string[9];
```

Assigning an array but not initializing the initial values will still initialize each element. The runtime initializes elements to their default values, as follows.

+   - Reference types (such as string) are initialized to null.
+   - Numeric types are initialized to zero.
+   - bool is initialized to false.
+   - char is initialized to '\0'.

Nonprimitive value types are recursively initialized by initializing each of their fields to their default values.

As a result, it is not necessary to individually assign each element of an array before using it.

In C# 2.0, it is possible to use the default() operator to determine the default value of a data type. default() takes a data type as a parameter. default(int), for example, returns 0 and default(char) returns \0.

Because the array size is not included as part of the variable declaration, it is possible to specify the size at runtime. For example, Listing 2.37 creates an array based on the size specified in the Console.ReadLine() call.

# LISTING 2.37: Defining the Array Size at Runtime

```
string[] groceryList;
System.Console.Write("How many items on the list? ");
int size = int.Parse(System.Console.ReadLine());
groceryList = new string[size];
// ...
```

C# initializes multidimensional arrays similarly. A comma separates the size of each rank. Listing 2.38 initializes a tic-tac-toe board with no moves.

# LISTING 2.38: Declaring a Two-Dimensional Array

```
int[,] cells = int[3,3];
```