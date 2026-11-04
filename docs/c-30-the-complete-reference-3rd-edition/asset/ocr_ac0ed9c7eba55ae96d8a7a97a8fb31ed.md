```
// Show the type of data used by iOb.
iOb.ShowType();

// Get the value in iOb.
int v = iOb.GetOb();
Console.WriteLine("value: " + v);

Console.WriteLine();

// Create a Gen object for strings.
Gen<string> strOb = new Gen<string>("Generics add power.");

// Show the type of data stored in strOb.
strOb.ShowType();

// Get the value in strOb.
string str = strOb.GetOb();
Console.WriteLine("value: " + str);
}
```

The output produced by the program is shown here:

```
Type of T is System.Int32
value: 102

Type of T is System.String
value: Generics add power.
```

Let's examine this program carefully.

First, notice how Gen is declared by the following line.

```
class Gen<T> {
```

Here, T is the name of a type parameter. This name is used as a placeholder for the actual type that will be specified when a Gen object is created. Thus, T is used within Gen whenever the type parameter is needed. Notice that T is contained within < >. This syntax can be generalized. Whenever a type parameter is being declared, it is specified within angle brackets. Because Gen uses a type parameter, Gen is a generic class.

In the declaration of Gen, there is no special significance to the name T. Any valid identifier could have been used, but T is traditional. Other commonly used type parameter names include V and E. Of course, you can also use descriptive names for type parameters, such as a TValue or TKey. When using a descriptive name, it is common practice to use T as the first letter.

Next, T is used to declare a variable called ob, as shown here:

```
T ob; // declare a variable of type T
```

As explained, T is a placeholder for the actual type that will be specified when a Gen object is created. Thus, ob will be a variable of the type bound to T when a Gen object is instantiated. For example, if type string is specified for T, then in that instance, ob will be of type string.