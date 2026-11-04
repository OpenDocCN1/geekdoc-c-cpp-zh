The following program creates a class called Item, which encapsulates an item’s name with its number. It creates another class called InStockStatus, which links an item number with a Boolean property that indicates whether or not the item is in stock. It also creates a class called Temp, which has two fields: one string and one bool. Objects of this class will hold the result of the query. The query uses join to produce a list in which an item’s name is associated with its in-stock status.

```
~~~csharp
// Demonstrate join.
using System;
using System.Linq;

// A class that links an item name with its number.
class Item {
    public string Name { get; set; }
    public int ItemNumber { get; set; }

    public Item(string n, int inum) {
        Name = n;
        ItemNumber = inum;
    }
}

// A class that links an item number with its in-stock status.
class InStockStatus {
    public int ItemNumber { get; set; }
    public bool InStock { get; set; }

    public InStockStatus(int n, bool b) {
        ItemNumber = n;
        InStock = b;
    }
}

// A class that encapsulates a name with its status.
class Temp {
    public string Name { get; set; }
    public bool InStock { get; set; }

    public Temp(string n, bool b) {
        Name = n;
        InStock = b;
    }
}

class JoinDemo {
    static void Main() {

        Item[] items = {
            new Item("Pliers", 1424),
            new Item("Hammer", 7892),
            new Item("Wrench", 8534),
            new Item("Saw", 6411)
        };
~~~
```