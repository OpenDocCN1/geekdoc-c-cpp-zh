```
setA.Add('B');
setA.Add('C');

setB.Add('C');
setB.Add('D');
setB.Add('E');

Show("Initial content of setA: ", setA);
Show("Initial content of setB: ", setB);

setA.SymmetricExceptWith(setB);
Show("setA after Symmetric difference with SetB: ", setA);

setA.UnionWith(setB);
Show("setA after union with setB: ", setA);

setA.ExceptWith(setB);
Show("setA after subtracting setB: ", setA);

Console.WriteLine();
}
```

The output is shown here:

Initial content of setA: A B C
Initial content of setB: C D E
setA after Symmetric difference with SetB: A B D E
setA after union with setB: A B D E C
setA after subtracting setB: A B

# Storing User-Defined Classes in Collections

For the sake of simplicity, the foregoing examples have stored built-in types, such as int, string, or char, in a collection. Of course, collections are not limited to the storage of built-in objects. Quite the contrary. The power of collections is that they can store any type of object, including objects of classes that you create.

Let's begin with an example that uses the non-generic class ArrayList to store inventory information that is encapsulated by the Inventory class:

```
// A simple inventory example.

using System;
using System.Collections;

class Inventory {
    string name;
    double cost;
    int onhand;

    public Inventory(string n, double c, int h) {
        name = n;
        cost = c;
        onhand = h;
```