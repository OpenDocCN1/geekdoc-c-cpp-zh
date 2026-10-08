# 14.2.1 An abstract class

Consider first **Shape**'s constructors:

```
protected:
  Shape() { }
  Shape(initializer_list<Point> lst);  // add() the Points to this Shape
```

The constructors are **protected**. That means that they can only be used directly from classes derived from **Shape** (using the `:Shape` notation). In other words, **Shape** can only be used as a base for classes, such as **Line** and **Open_polyline**. The purpose of **protected:** is to ensure that we don't make **Shape** objects directly. For example:

```
Shape ss;      // error: cannot construct Shape
```

**Shape** is designed to be a base class only. In this case, nothing particularly nasty would happen if we allowed people to create **Shape** objects directly, but by limiting use, we keep open the possibility of modifications to **Shape** that would render it unsuitable for direct use. Also, by prohibiting the direct creation of **Shape** objects, we directly model the idea that we cannot have/see a general shape, only particular shapes, such as **Circle** and **Closed_polyline**. Think about it! What does a shape look like? The only reasonable response is the counter question "What shape?" The notion of a shape that we represent by **Shape** is an abstract concept. That's an important and frequently useful design notion, so we don't want to compromise it in our program. Allowing users to directly create **Shape** objects would do violence to our ideal of classes as direct representations of concepts.

The default constructor sets the members to their default values. Here again, the underlying library used for implementation, FLTK, "shines through." However, FLTK's notions of color and style are not mentioned directly by the user. They are only part of the implementation of our **Shape**, **Color**, and **Line_style** classes. The **vector<Point>** defaults to an empty vector.

The initializer-list constructor also uses the default initializers, and then **add()**s the elements of its argument list to the **Shape**:

```
Shape::Shape(initializer_list<Point> lst)
{
  for (Point p : lst) add(p);
}
```

A class is *abstract* if it can be used only as a base class. The other - more common - way of achieving that is called a *pure virtual function*; see §14.3.5. A class that can be used to create objects - that is, the opposite of an abstract class - is called