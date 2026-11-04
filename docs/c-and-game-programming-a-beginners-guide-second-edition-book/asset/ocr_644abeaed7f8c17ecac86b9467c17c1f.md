Component number [5] is not a usable variable and instead holds the null character that terminates the line. Additional indexed variables (for example, number [6], [7]), will also exceed the array's declared space, which may not be flagged as a compilation error.

> > **Note**
> >
> > In Example 4.2, the first value is zero (not one).² In addition, you might conclude that this array should hold six values since number [5] was not used. This conclusion would be in error since C#, like C/C++ before it, withholds that last space as a termination marker. C#, however, does not use the zero-null character namely "\0" to assign that value. Our first chore then will be to convert a simple singular variable program into one that can take advantage of the new array format (the potential of arrays will become obvious very shortly).

# ## Declaring and Referencing Arrays

The declaration of an array doesn't vary greatly from the declaration of either a standard or a constant variable. They are generally written using lowercase lettering, and all of the rules of variable naming still apply. The one significant difference is in the insertion of the square brackets (demonstrated in the last example), which both define an array and allow us to reference its components. The capacity of an array is determined by the size of the value placed inside those initializing brackets. The formal name for this type of value is the *indexed variable*, but it is also known as the *subscripted variable*, or less precisely, as an *element* (i.e., an element of an array). The number of indexed variables (total spaces reserved) is called the *declared size*, or just the size, while the data type used to declare that array is called the *base type* (see Examples 4.3 and 4.4).

# ### Example 4.3. Converting from singular variables to an array—part 1.

```
```csharp
using System;

namespace Chapter4 {
    class Class1 {
        static void Main() {
            string input;

            char student0, student1, student2, student3, student4;
```
```

² In C#, as with C/C++ and assembled languages, the array's numeric notation can be seen as a measure of the distance from one space in the array to another. Since the first space has no space or distance from itself this would in fact be noted as zero. Although it is possible for higher-level languages to alter this vr...