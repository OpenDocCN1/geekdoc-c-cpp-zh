program more brittle. The fundamental problem with creating classes that can work with multiple data types without generics is that they must work with a common base class (or interface), usually object.

Using value types, such as a struct or an integer, with classes that use object exacerbates the problem. If you pass a value type to the Stack.Push() method, for example, the runtime automatically boxes it. Similarly, when you retrieve a value type, you need to explicitly unbox the data and cast the object reference you obtain from the Pop() method into a value type. Casting a reference type to a base class or interface has a negligible performance impact, but the box operation for a value type introduces more overhead, because it must allocate memory, copy the value, and then later garbage-collect that memory.

C# is a language that encourages type safety: The language is designed so that many type errors, such as assigning an integer to a variable of type string, can be caught at compile time. The fundamental problem is that the Stack class is not as type-safe as one expects a C# program to be. To change the Stack class to enforce type safety to restrict the contents of the stack to be a particular data type (without using generic types), you must create a specialized stack class, as in Listing 12.3.

# **LISTING 12.3: Defining a Specialized Stack Class**

```
```csharp
public class CellStack
{
public virtual Cell Pop();
public virtual void Push(Cell cell);
// ... 
}
```
```

Because CellStack can store only objects of type Cell, this solution requires a custom implementation of the stack methods, which is less than ideal. Implementing a type-safe stack of integers would require yet another custom implementation; each implementation would look remarkably like every other one. There would be lots of duplicated, redundant code.