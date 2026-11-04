This method compares obj1 with obj2 and returns greater than zero if obj1 is greater than obj2, zero if the two objects are the same, and less than zero if obj1 is less than obj2.

Here is a generic version of the preceding program that uses IComparer<T>. It produces the same output as the previous versions of the program.

```
```csharp
// Use IComparer<T>.

using System;
using System.Collections.Generic;

// Create an IComparer<T> for Inventory objects.
class CompInv<T> : IComparer<T> where T : Inventory {

    // Implement the IComparer<T> interface.
    public int Compare(T obj1, T obj2) {
        return obj1.name.CompareTo(obj2.name);
    }
}

class Inventory {
    public string name;
    double cost;
    int onhand;

    public Inventory(string n, double c, int h) {
        name = n;
        cost = c;
        onhand = h;
    }

    public override string ToString() {
        return
            String.Format("{0,-10}Cost: {1,6:C}  On hand: {2}",
                          name, cost, onhand);
    }
}

class GenericIComparerDemo {
    static void Main() {
        CompInv<Inventory> comp = new CompInv<Inventory>();
        List<Inventory> inv = new List<Inventory>();

        // Add elements to the list.
        inv.Add(new Inventory("Pliers", 5.95, 3));
        inv.Add(new Inventory("Wrenches", 8.29, 2));
        inv.Add(new Inventory("Hammers", 3.50, 4));
        inv.Add(new Inventory("Drills", 19.88, 8));

        Console.WriteLine("Inventory list before sorting:");
        foreach(Inventory i in inv) {
            Console.WriteLine("   " + i);
        }
        Console.WriteLine();
    }
}
```
```