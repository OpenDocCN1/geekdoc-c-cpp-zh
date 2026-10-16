## Quick Primer

- Structs and classes are very similar to one another.
- The struct is created with the struct keyword rather than the class keyword.
- Structs are created on the Stack, not on the Heap and this makes them perform faster but it also leads to them being passed by value and not reference.

## What's Next?

While the struct and the class are similar, they do have differences, with the main one being allocation of the struct on the Stack and not the Heap. As this means it is passed by value, the method gets a copy of the struct, not the original.

It is a nice feature and you do need to know about them but the likelihood is you will use classes way more than you ever will use a struct.

Next, we are going to delve into inheritance.

## Inheritance

Let’s imagine that you have many geometric polygons that you want to track. That would include squares, triangles, rectangles, pentagons, and so on. You could create a class called Polygon that contains the number of sides on the polygon and perhaps also has an array in it that contains the vertices or corner positions of the polygon.

You could use this Polygon class to represent any one of the polygons but, using a square as an example, you might want to do something else with it. For instance, you might want to create a square using a single size – the height and width of a square are the same lengths – or you might want to create a method to return the square area.

One way of doing it would be to create a class called Square and this class would contain everything from the Polygon class but everything else you need. So, what’s the problem?

The problem is that you now have a class that is completely different and you if wanted to change how polygons were worked with, you would also need to change how squares are worked with. On top of that, while you could have an array of polygons (Polygon[] polygon) there is no way of adding squares to it - yes, I know that a square is a polygon and we should be able to treat it as such.

This leads us to the section on inheritance.

A square is most definitely a polygon but it is a bit more specific than that – a square is a special polygon type that has special attributes. Whatever a polygon can do, a square can do it too because, yes, that square is a polygon.

This is known, in programming circles, as an ‘is-a’ type of relationship and it is such a common thing that most programming languages facilitate it by creating constructs.

The C# construct that lets us do this is known as inheritance and this lets us create that class called Polygon and create a class called

Square based on our Polygon class; from this, we can reuse everything in the Polygon class. So, any changes made to Polygon would be reflected automatically in our Square class.

### Base Classes

Base classes are often also called parent classes or super-classes. We’ll stick with calling them base classes for now. A base class is much like a standard class but it is used for the purposes of inheritance by another class. In our case, the base class is the Polygon class.

For example, our class could look like this:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace Inheritance
{
    class Polygon
    {
        public int NumberOfSides { get; set; }

        public Polygon()
        {
            NumberOfSides = 0;
        }

        public Polygon(int numberOfSides)
{
    NumberOfSides = numberOfSides;
}
}
}
```

### Derived Classes

Derived classes are also known as subclasses and are based on other classes. Our Square class is a class that was derived from the Polygon class. Derived classes are created in much the same way as a standard class but with one difference – that difference is what tells the program which of our classes is the base class.

A standard class is created like this:

```
class Square
{
    //...
}
```

The colon (:) is used as an indication that the Square class has been derived from our Polygon class; this is followed by the base class name:

```
class Square : Polygon
{
    //...
}
```

All we do in the class is to indicate anything new for the Square class that is not in the Polygon class. Our Square class will look like this:

```
using System;
using System.Collections.Generic;
using System.Linq;
```

```
Square square = new Square(4.5f); // a square, which is a polygon that has 4 sides of length 4.5.
```

However, our Square is already a Polygon so you could also include a variable with a type of Polygon that stores a Square. Are you still with me?

```
Polygon polygon = new Square(4.5f);
```

While the program is running and while the Polygon variable is being used, we can only access what is inside Polygon. What we could do is check what NumberOfSides is but we would not be able to find out if a Square or a Polygon, or any other type, perhaps a parallelogram, is being tracked by a variable of Polygon type. All we know is that it is a Polygon and all we can work with is what the Polygon has.

### Checking Type and Casting for Objects

As we just discussed, we can work with derived types, such as Square, but we can only know what it is – a Polygon. There will be times that we will want to work out what an object type is so we can work with it in a different way. We can do this by using the ‘is’ keyword and using casting:

```
Polygon polygon = new Square(4.5f);
```

```
if (polygon is Square)
{
	Square square = (Square)polygon;
	// Now we can do whatever we want with the square.
}
```

### Using Inheritance in Arrays

One more thing that we should talk about is creating arrays of the base class. An example of that would be Polygon[] lotsOfPolygons = new Polygon[5];. Then we could put a derived class in it – lotsOfPolygons[2] = new Square(92.1f);.

Derived classes are able to function the same way as their bases classes do.

### Constructors and Inheritance

All the properties, methods, and instance variables in a derived class are inherited. The constructor is somewhat different.

Constructors from a base class cannot be used to create derived classes. For example, the constructor in the Polygon class is able to take an int as the value of the number of sides but a Square cannot be created from that constructor.

There is a good reason for that — it makes no sense. If you could use something along the lines of `Square square = new Polygon(6);` to create a new Square, setting it as 6 sides, it would all be a bit messy.

Object instances can only be created from constructors defined by the derived class.

There’s more to the constructor - because derived classes have been based on other classes, we would also need to get a constructor from the base class and the default is the construction with no parameters – the Polygon(), for example.

Don’t forget, whether you have declared constructors or not, the compiler will create a constructor with no parameters by default.

You don’t need to use this if you don’t want to or you may have a base class that does not have one of these parameterless constructors.

Either way, you have the choice of any constructor for the base class in the constructors for the derived class and for that, you use the base keyword. The constructor we created in the Square class originally would be defined like this:

```
public Square(float size)
    : base(4)
{

```
```
Size = size;
```

```
}
```

We add a colon and the base keyword together with the base class parameters that we want to make use of. By doing this, we can get rid of the parameterless constructor from the Polygon class – this constructor is responsible for letting programmers create Polygons with no number of sides specified!

### Protected Access Modifier

Previously, we talked about the public and the private access modifier; public means that the variable or method is available to anyone, while private means it can only be accessed from within the class to which the variable or method belongs.

Inheritance gives us a third option – the protected access modifier. If you mark a method, variable, or property as protected rather than public or private, it can only be accessed from within the class or any class derived from that class.

So, if the NumberOfSides property in our Polygon class was protected rather than public, it could be accessed from the Polygon class, the Square class, and any other derived class but not from anywhere else.

### The Base Class of Everything

Even if you didn’t specify a class for inheritance purposes, every class you create is already derived from a base class. This is the base class of everything and it is the class called object.

There is also an object keyword that works much the same as the float or int types we’ve used but the object keyword always represents objects. And, because it is a class, it is a reference type and not a value type. However, the inheritance properties dictate that it can be used for representing any object.

Remember earlier, when I said that you could store derived classes in base types, like this:
