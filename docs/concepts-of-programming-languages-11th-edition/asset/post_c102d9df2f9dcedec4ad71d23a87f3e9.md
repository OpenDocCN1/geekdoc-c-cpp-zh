
references must include the variable that references the inner class object. For example, suppose the outer class creates an instance of the inner class with the following statement:

```
myInner = this.new Inner();
```

Then, if the inner class defines a variable named *sum*, it can be referenced in the outer class as *myInner.sum*.

An instance of a nested class can only exist within an instance of its nesting class. Nested classes can also be anonymous. Anonymous nested classes have complex syntax but are really only an abbreviated way to define a class that is used from just one location. An example of an anonymous nested class appears in Chapter 14.

A local nested class is defined in a method of its nesting class. Local nested classes are never defined with an access specifier (**private** or **public**). Their scope is always limited to their nesting class. A method in a local nested class can access the variables defined in its nesting class and the *final* variables defined in the method in which the local nested class is defined. The members of a local nested class are visible only in the method in which the local nested class is defined.

#### 12.4.4.5 Evaluation

Java's design for supporting object-oriented programming is similar to that of C++, but it employs more consistent adherence to object-oriented principles. Java does not allow parentless classes and uses dynamic binding as the "normal" way to bind method calls to method definitions. This, of course, increases execution time slightly over languages in which many method bindings are static. At the time this design decision was made, however, most Java programs were interpreted, so interpretation time made the extra binding time insignificant. Access controls for the contents of a class definition are rather simple when compared with the jungle of access controls of C++, ranging from derivation controls to friend functions. Finally, Java uses interfaces to provide a form of support for multiple inheritance, which does not have all of the drawbacks of actual multiple inheritance.

### 12.4.5 C#

C#'s support for object-oriented programming is similar to that of Java.

#### 12.4.5.1 General Characteristics

C# includes both classes and structs, with the classes being very similar to Java's classes and the structs being somewhat less powerful constructs. One important difference is that structs are value types; that is, they are stack dynamic. This could cause the problem of object slicing, but this is prevented by the restriction that structs cannot be subclassed. More details of how C# structs differ from its classes appeared in Chapter 11.

#### 12.4.5.2 Inheritance

C# uses the syntax of C++ for defining classes. For example,

```csharp
public class NewClass : ParentClass { . . . }
```

A method inherited from the parent class can be replaced in the derived class by marking its definition in the subclass with `new`. The `new` method hides the method of the same name in the parent class to normal access. However, the parent class version can still be called by prefixing the call with `base`. For example,

```csharp
base.Draw();
```

As with Java, subclasses can be subtypes. C#’s support for interfaces is the same as that of Java. It does not support multiple inheritance.

#### 12.4.5.3 Dynamic Binding

To allow dynamic binding of method calls to methods in C#, both the base method and its corresponding methods in derived classes must be specially marked. The base class method must be marked with `virtual`, as in C++. To make clear the intent of a method in a subclass that has the same name and protocol as a virtual method in an ancestor class, C# requires that such methods be marked `override` if they are to override the parent class virtual method.^14 For example, the C# version of the C++ `Shape` class that appears in Section 12.4.2.3 is as follows:

```csharp
public class Shape {
    public virtual void Draw() { . . . }
    . . .
}
public class Circle : Shape {
    public override void Draw() { . . . }
    . . .
}
public class Rectangle : Shape {
    public override void Draw() { . . . }
    . . .
}
public class Square : Rectangle {
    public override void Draw() { . . . }
    . . .
}
```

C# includes abstract methods similar to those of C++, except that they are specified with different syntax. For example, the following is a C# abstract method:

```csharp
abstract public void Draw();
```

A class that includes at least one abstract method is an abstract class, and every abstract class must be marked `abstract`. Abstract classes cannot be instantiated. It follows that any subclass of an abstract class that will be instantiated must implement all abstract methods that it inherits.

As with Java, all C# classes are ultimately derived from a single root class, `Object`. The `Object` class defines a collection of methods, including `ToString`, `Finalize`, and `Equals`, which are inherited by all C# types.

#### 12.4.5.4 Nested Classes

A C# class that is directly nested in a class behaves like a Java static nested class (which is like a nested class in C++). Like C++, C# does not support nested classes that behave like the nonstatic nested classes of Java.

#### 12.4.5.5 Evaluation

Because C# is a recently designed C-based object-oriented language, one should expect that its designers learned from their predecessors and duplicated the successes of the past and remedied some of the problems. One result of this, coupled with the few problems with Java, is that the differences between C#’s support for object-oriented programming and that of Java are relatively minor. The availability of structs in C#, which Java does not have, can be considered an improvement. Like that of Java, C#’s support for object-oriented programming is simpler than that of C++, which many consider an improvement.

### 12.4.6 Ruby

As stated previously, Ruby is a pure object-oriented programming language in the sense of Smalltalk. Virtually everything in the language is an object and all computation is accomplished through message passing. Although programs have expressions that use infix operators and therefore have the same appearance as expressions in languages like Java, those expressions are actually evaluated through message passing. As is the case with Smalltalk, when one writes `a + b`, it is evaluated by sending the message `+` to the object referenced by `a`, passing a reference to the object `b` as a parameter. In other words, `a + b` is implemented as `a.+ b`.

#### 12.4.6.1 General Characteristics

Ruby class definitions differ from those of languages such as C++ and Java in that they are executable. Because of this, they are allowed to remain open during execution. A program can add members to a class any number of times, simply by providing secondary definitions of the class that include the new members. During execution, the current definition of a class is the union of all definitions of the class that have been executed. Method definitions are

two instance variables, @one and @two, those getters can be specified with the single statement in the class:

```
attr_reader :one, :two
```

attr_reader is actually a function call, using :one and :two as the actual parameters. Preceding a variable with a colon (:) causes the variable name to be used, rather than dereferencing it to the object to which it refers. Instead of passing a value or an address, the text of the variable's name is passed. This is exactly how macro parameters are passed.

The function that similarly creates setters is called attr_writer. This function has the same parameter profile as attr_reader.

The functions for creating getter and setter methods are so named because they provide the protocol for objects of the class, which then are called attributes. So, the attributes of a class define the data interface (the data made public through accessor methods) to objects of the class.

Class variables, which are specified by preceding their names with two at signs (@@), are private to the class and its instances. That privacy cannot be changed. Also, unlike global and instance variables, class variables must be initialized before they are used.

#### 12.4.6.2 Inheritance

Subclasses are defined in Ruby using the less-than symbol (<), rather than the colon of C++. For example,

```
class MySubClass < BaseClass
```

One distinct thing about the method access controls of Ruby is that they can be changed in a subclass, simply by calling the access control functions. This means that two subclasses of a base class can be defined so that objects of one of the subclasses can access a method defined in the base class, but objects of the other subclass cannot. Also, this allows one to change the access of a publicly accessible method in the base class to a privately accessible method in the subclass.

#### 12.4.6.3 Dynamic Binding

Support for dynamic binding in Ruby is the same as it is in Smalltalk. Variables are not typed; rather, they are all references to objects of any class. So, all variables are polymorphic and all bindings of method calls to methods are dynamic.

#### 12.4.6.4 Evaluation

Because Ruby is an object-oriented programming language in the purest sense, its support for object-oriented programming is obviously adequate. However, access control to class members is weaker than that of C++. Ruby does not
