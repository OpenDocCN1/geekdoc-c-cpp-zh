
```
static void Main() {
    MyStruct a;
    MyStruct b;

    a.x = 10;
    b.x = 20;

    Console.WriteLine("a.x {0}, b.x {1}", a.x, b.x);

    a = b;
    b.x = 30;

    Console.WriteLine("a.x {0}, b.x {1}", a.x, b.x);
}
```

The output is shown here:

```
a.x 10, b.x 20
a.x 20, b.x 30
```

As the output shows, after the assignment

```
a = b;
```

the structure variables a and b are still separate and distinct. That is, a does not refer to or relate to b in any way other than containing a copy of b's value. This would not be the case if a and b were class references. For example, here is the class version of the preceding program:

```
// Use a class.

using System;

// Now a class.
class MyClass {
    public int x;
}

// Now show a class object assignment.
class ClassAssignment {
    static void Main() {
        MyClass a = new MyClass();
        MyClass b = new MyClass();

        a.x = 10;
        b.x = 20;

        Console.WriteLine("a.x {0}, b.x {1}", a.x, b.x);

        a = b;
        b.x = 30;
        Console.WriteLine("a.x {0}, b.x {1}", a.x, b.x);
    }
}
```

The output from this version is shown here:

a.x 10, b.x 20
a.x 30, b.x 30

As you can see, after the assignment of b to a, both variables refer to the same object—the one originally referred to by b.

## Why Structures?

At this point, you might be wondering why C# includes the struct since it seems to be a less-capable version of a class. The answer lies in efficiency and performance. Because structures are value types, they are operated on directly rather than through a reference. Thus, a struct does not require a separate reference variable. This means that less memory is used in some cases. Furthermore, because a struct is accessed directly, it does not suffer from the performance loss that is inherent in accessing a class object. Because classes are reference types, all access to class objects is through a reference. This indirection adds overhead to every access. Structures do not incur this overhead. In general, if you need to simply store a group of related data, but don’t need inheritance and don’t need to operate on that data through a reference, then a struct can be a more efficient choice.

Here is another example that shows how a structure might be used in practice. It simulates an e-commerce transaction record. Each transaction includes a packet header that contains the packet number and the length of the packet. This is followed by the account number and the amount of the transaction. Because the packet header is a self-contained unit of information, it is organized as a structure. This structure can then be used to create a transaction record, or any other type of information packet.

```
// Structures are good when grouping small amounts of data.

using System;

// Define a packet structure.
struct PacketHeader {
    public uint PackNum; // packet number
    public ushort PackLen; // length of packet
}

// Use PacketHeader to create an e-commerce transaction record.
class Transaction {
    static uint transacNum = 0;

    PacketHeader ph; // incorporate PacketHeader into Transaction
    string accountNum;
    double amount;

    public Transaction(string acc, double val) {
        // create packet header
        ph.PackNum = transacNum++;
        ph.PackLen = 512; // arbitrary length

        accountNum = acc;
        amount = val;
    }

    // Simulate a transaction.
    public void sendTransaction() {
        Console.WriteLine("Packet #: " + ph.PackNum +
            ", Length: " + ph.PackLen +
            "\n Account #: " + accountNum +
            ", Amount: {0:C}\n", amount);
    }
}

// Demonstrate Packet.
class PacketDemo {
    static void Main() {
        Transaction t = new Transaction("31243", -100.12);
        Transaction t2 = new Transaction("AB4655", 345.25);
        Transaction t3 = new Transaction("8475-09", 9800.00);

        t.sendTransaction();
        t2.sendTransaction();
        t3.sendTransaction();
    }
}
```

The output from the program is shown here:

```
Packet #: 0, Length: 512,
    Account #: 31243, Amount: ($100.12)

Packet #: 1, Length: 512,
    Account #: AB4655, Amount: $345.25

Packet #: 2, Length: 512,
    Account #: 8475-09, Amount: $9,800.00
```

PacketHeader is a good choice for a struct because it contains only a small amount of data and does not use inheritance or even contain methods. As a structure, PacketHeader does not incur the additional overhead of a reference, as a class would. Thus, any type of transaction record can use PacketHeader without affecting its efficiency.

As a point of interest, C++ also has structures and uses the struct keyword. However, C# and C++ structures are not the same. In C++, struct defines a class type. Thus, in C++, struct and class are nearly equivalent. (The difference has to do with the default access of their members, which is private for class and public for struct.) In C#, a struct defines a value type, and a class defines a reference type.

## Enumerations

An enumeration is a set of named integer constants. The keyword enum declares an
enumerated type. The general form for an enumeration is

```
    enum name { enumeration list };
```

Here, the type name of the enumeration is specified by name. The enumeration list is a
comma-separated list of identifiers.

Here is an example. It defines an enumeration called Apple that enumerates various
types of apples:

```
    enum Apple { Jonathan, GoldenDel, RedDel, Winesap,
                 Cortland, McIntosh };
```

A key point to understand about an enumeration is that each of the symbols stands for
an integer value. However, no implicit conversions are defined between an enum type and
the built-in integer types, so an explicit cast must be used. Also, a cast is required when
converting between two enumeration types. Since enumerations represent integer values,
you can use an enumeration to control a switch statement or as the control variable in a for
loop, for example.

Each enumeration symbol is given a value one greater than the symbol that precedes it.
By default, the value of the first enumeration symbol is 0. Therefore, in the Apple enumeration,
Jonathan is 0, GoldenDel is 1, RedDel is 2, and so on.

The members of an enumeration are accessed through their type name via the dot
operator. For example

```
    Console.WriteLine(Apple.RedDel + " has the value " +
                 (int)Apple.RedDel);
```

displays

```
    RedDel has the value 2
```

As the output shows, when an enumerated value is displayed, its name is used. To obtain
its integer value, a cast to int must be employed.

Here is a program that illustrates the Apple enumeration:

```
    // Demonstrate an enumeration.

    using System;

    class EnumDemo {
        enum Apple { Jonathan, GoldenDel, RedDel, Winesap,
                     Cortland, McIntosh };

        static void Main() {
            string[] color = {
                "Red",
                "Yellow",
                "Red",
                "Red",
                "Red",
                "Reddish Green"
            };

            Apple i; // declare an enum variable

            // Use i to cycle through the enum.
            for(i = Apple.Jonathan; i <= Apple.McIntosh; i++)
                Console.WriteLine(i + " has value of " + (int)i);

            Console.WriteLine();

            // Use an enumeration to index an array.
            for(i = Apple.Jonathan; i <= Apple.McIntosh; i++)
                Console.WriteLine("Color of " + i + " is " +
                    color[(int)i]);
        }
    }
```

The output from the program is shown here:

```
Jonathan has value of 0
GoldenDel has value of 1
RedDel has value of 2
Winesap has value of 3
Cortland has value of 4
McIntosh has value of 5

Color of Jonathan is Red
Color of GoldenDel is Yellow
Color of RedDel is Red
Color of Winesap is Red
Color of Cortland is Red
Color of McIntosh is Reddish Green
```

Notice how the for loops are controlled by a variable of type Apple. Because the enumerated values in Apple start at zero, these values can be used to index color to obtain the color of the apple. Notice that a cast is required when the enumeration value is used to index the color array. As mentioned, there are no implicit conversions defined between integers and enumeration types. An explicit cast is required.

### Initialize an Enumeration

You can specify the value of one or more of the symbols by using an initializer. Do this by following the symbol with an equal sign and an integer value. Symbols that appear after initializers are assigned values greater than the previous initialization value. For example, the following code assigns the value of 10 to RedDel:

```
enum Apple { Jonathan, GoldenDel, RedDel = 10, Winesap,
    Cortland, McIntosh };
```
