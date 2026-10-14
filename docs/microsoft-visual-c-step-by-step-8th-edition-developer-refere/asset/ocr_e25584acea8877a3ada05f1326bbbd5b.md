Clone method for the Circle class could be defined as shown here:

Click here to view code image

```
class Circle
{
    private int radius;
    // Constructors and other methods omitted
    ...
    public Circle Clone()
    {
        // Create a new Circle object
        Circle clone = new Circle();

        // Copy private data from this to clone
        clone.radius = this.radius;

        // Return the new Circle object containing the copied data
        return clone;
    }
}
```

This approach is straightforward if all the private data consists of values, but if one or more fields are themselves reference types (for example, the Circle class might be extended to contain a Point object from Chapter 7, indicating the position of the Circle on a graph), these reference types also need to provide a Clone method; otherwise, the Clone method of the Circle class will simply copy a reference to these fields. This process is known as a deep copy. The alternative approach, wherein the Clone method simply copies references, is known as a shallow copy.

The preceding code example also poses an interesting question: How private is private data? Previously, you saw that the private keyword renders a field or method inaccessible from outside a class. However, this does not mean it can be accessed by only a single object. If you create two objects of the same class, they can each access the private data of the other within the code for that class. This sounds curious, but in fact, methods such as Clone depend on this feature. The statement clone.radius = this.radius; works only because the private radius field in the clone object is accessible from within the current instance of the Circle class. So, private actually means “private to the class” rather than “private to an object.” However, don’t confuse private with static. If you simply declare a field as private, each instance of the class gets its own data. If a field is declared as static, each instance of the class shares the same data.

# Use value parameters and reference parameters

+   1. Start Microsoft Visual Studio 2015 if it is not already running.