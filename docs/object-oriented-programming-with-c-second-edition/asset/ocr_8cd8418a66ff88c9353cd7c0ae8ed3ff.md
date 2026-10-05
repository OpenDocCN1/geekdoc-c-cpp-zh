# Appendix C: Comparison of C++ with Java 433

+   - The default base class in Java: If you do not specify a base class for a class you are defining, the Java compiler automatically assigns a class called Object as its base class. Therefore, all classes in Java inherit from the class Object.

+   - Overriding member functions of a base class in its derived classes: Using the final keyword in the declaration of the member function of a class prevents the derived class from overriding it. The compiler throws an error if a member function of the derived class overrides a final method of the base class.

+   - Interfaces and abstract base classes: An interface in Java is similar to the abstract class in C++ but with the following differences:

+   - Member functions of an interface can only be declared. They cannot be defined.

+   - Member data of an interface are considered final.

An interface is declared in Java as follows:

```
public interface A {
    public void abc();           //declaration only - no definition
    public void def();          //declaration only - no definition
}
```

Like the abstract classes of C++, interfaces in Java cannot be instantiated.

A a = new A();

A class that implements an interface can be instantiated provided it defines all member functions of the interface. See Listing C.6.

# Listing C.6 Declaring and implementing an interface in Java

```
public class B implements A      //syntax for implementing an
    //interface
    public void abc() {
        /*
        definition of the function
        */
}
```

If not all member functions of the interface are defined in the class that implements them, the class becomes an abstract base class and cannot be instantiated.

Multiple inheritance is not supported in Java. However, Java provides interfaces. A class in Java can inherit from only one class but implement an unlimited number of interfaces. In the following definition, class X inherits from class P but implements the interfaces A and B.

```
//implementing more than one interface
public class X extends P implements A, B {
    /*
    definition of class X
    */
}
```