# 13.6.1 Subclass Constructor

A subclass constructor is used to construct the instance variables of both the subclass and the superclass. The subclass constructor uses the keyword base to invoke the constructor method of the superclass.

```
public BedRoom (int x, int y, int z) : base (x, y)
{
    height = z;
}
```

Here, the derived constructor takes three arguments, the first two to provide values to the base constructor and the third one to provide value to its own class member. Note that base (x,y) behaves like a method call and therefore arguments are specified without types. The type and order of these arguments must match the type and order of base constructor arguments.

When the compiler encounters base (x,y), it passes the values x and y to the base class constructor which takes two int arguments. The base class constructor is called before the derived class constructor is executed. That is, the data members length and breadth are assigned values before the member height is assigned its value.

Note that the use of keyword base is not limited to the constructor logic alone. We may use the base in any subclass to access a public or protected member defined in a parent class. For instance, statements such as:

```
base.length = 100;
int area = base.Area();
```

are valid inside the derived class Bedroom.

# 13.7 MULTILEVEL INHERITANCE

A common requirement in object-oriented programming is the use of a derived class as a superclass. C# supports this concept and uses it extensively in building its class library. This concept allows us to build a chain of classes as shown in Fig. 13.5.

The class A serves as a base class for the derived class B which in turn serves as a base class for the derived class C. The chain ABC is known as inheritance path.

A derived class with multilevel base classes is declared as follows:

```
class A
{
    ....
    ....
}
class B : A // First level derivation
{
    ....
    ....
}
class C : B // Second level derivation
{
    ....
```

![](bbox=[0.58, 0.77, 0.92, 0.87])

Fig. 13.5 Multilevel inheritance