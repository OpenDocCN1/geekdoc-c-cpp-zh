```
{
    Rectangle Rect = new Rectangle();
    Rect.setWidth(5);
    Rect.setHeight(7);
    // Print the area of the object.
    Console.WriteLine("Total area: {0}", Rect.getArea());
    Console.ReadKey();
}
}
}
```

On executing the code shown above, the following result can be achieved.

Total area: 35

# Initialization of a Base Class

As you know, the derived class will inherit the member methods and member variables of the base class. As such, it is necessary to create the super class object before the creation of the subclass. Instructions for the initialization of the superclass can be provided in the member initialization list.

The following example illustrates this.