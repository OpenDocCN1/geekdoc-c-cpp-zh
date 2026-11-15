+   * Derived/sub/child type: The specialized type that inherits the members of the more general type.

+   * Base/super/parent type: The general type whose members a derived type inherits.

Inheritance forms an “is a” relationship. The derived type is always implicitly also of the base type. Just as a hard drive “is a” storage device, any other type derived from the storage device type “is a” type of storage device.

# Derivation

It is common to want to extend a given type to add features, such as behavior and data. The purpose of inheritance is to do exactly that. Given a Person class, you create an Employee class that additionally contains EmployeeId and Department properties. The reverse approach may also occur. Given, for example, a Contact class within a Personal Digital Assistant (PDA), you decide you also can add calendaring support. Toward this effort, you create an Appointment class. However, instead of redefining the methods and properties that are common to both classes, you refactor the Contact class. Specifically, you move the common methods and properties on Contact into a base class called PdaItem from which both Contact and Appointment derive, as shown in Figure 6.1.

The common items in this case are Created, LastUpdated, Name, ObjectKey, and the like. Through derivation, the methods defined on the base class, PdaItem, are accessible from all subclasses of PdaItem.

When defining a derived class, follow the class identifier with a colon and then the base class, as Listing 6.1 demonstrates.

```
LISTING 6.1: Deriving One Class from Another
public class PdaItem
{
    public string Name { get; set; }
    public DateTime LastUpdated { get; set; }
}
```