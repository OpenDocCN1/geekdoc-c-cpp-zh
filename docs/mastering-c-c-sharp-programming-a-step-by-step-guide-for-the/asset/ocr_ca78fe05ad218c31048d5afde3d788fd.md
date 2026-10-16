```
Square square = new Square(4.5f); // a square, which is a polygon that has 4 sides of length 4.5.
```

However, our Square is already a Polygon so you could also include a variable with a type of Polygon that stores a Square. Are you still with me?

```
Polygon polygon = new Square(4.5f);
```

While the program is running and while the Polygon variable is being used, we can only access what is inside Polygon. What we could do is check what NumberOfSides is but we would not be able to find out if a Square or a Polygon, or any other type, perhaps a parallelogram, is being tracked by a variable of Polygon type. All we know is that it is a Polygon and all we can work with is what the Polygon has.

# Checking Type and Casting for Objects

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

# Using Inheritance in Arrays

One more thing that we should talk about is creating arrays of the base class. An example of that would be Polygon[] lotsOfPolygons = new Polygon[5];. Then we could put a derived class in it – lotsOfPolygons[2] = new Square(92.1f);.