Interfaces are declared by using the interface keyword. Here is a simplified form of an interface declaration:

```
interface name {
    ret-type method-name1(param-list);
    ret-type method-name2(param-list);
    // ...
    ret-type method-nameN(param-list);
}
```

The name of the interface is specified by name. Methods are declared using only their return type and signature. They are, essentially, abstract methods. As explained, in an interface, no method can have an implementation. Thus, each class that includes an interface must implement all of the methods. In an interface, methods are implicitly public, and no explicit access specifier is allowed.

Here is an example of an interface. It specifies the interface to a class that generates a series of numbers.

```
public interface ISeries {
    int GetNext(); // return next number in series
    void Reset(); // restart
    void SetStart(int x); // set starting value
}
```

The name of this interface is ISeries. Although the prefix I is not necessary, many programmers prefix interfaces with I to differentiate them from classes. ISeries is declared public so that it can be implemented by any class in any program.

In addition to methods, interfaces can specify properties, indexers, and events. Events are described in Chapter 15, and we will be concerned with only methods, properties, and indexers here. Interfaces cannot have data members. They cannot define constructors, destructors, or operator methods. Also, no member can be declared as static.

# Implementing Interfaces

Once an interface has been defined, one or more classes can implement that interface. To implement an interface, the name of the interface is specified after the class name in just the same way that a base class is specified. The general form of a class that implements an interface is shown here:

```
class class-name : interface-name {
    // class-body
}
```

The name of the interface being implemented is specified in interface-name. When a class implements an interface, the class must implement the entire interface. It cannot pick and choose which parts to implement, for example.

A class can implement more than one interface. When a class implements more than one interface, specify each interface in a comma-separated list. A class can inherit a base class and also implement one or more interfaces. In this case, the name of the base class must come first in the comma-separated list.