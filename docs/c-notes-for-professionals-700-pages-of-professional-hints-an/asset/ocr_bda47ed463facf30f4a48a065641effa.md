```
```csharp
public string Area(double width, double height) { ... }
public double Area(double width, double height) { ... }
// This will NOT compile.
```
```

If we need to have our class use the same method names that return different values, we can remove the issues of ambiguity by implementing an interface and explicitly defining its usage.

```
```csharp
public interface IAreaCalculatorString {
    public string Area(double width, double height);
}

public class AreaCalculator : IAreaCalculatorString {
    public string IAreaCalculatorString.Area(double width, double height) { ... }
    // Note that the method call now explicitly says it will be used when called through
    // the IAreaCalculatorString interface, allowing us to resolve the ambiguity.
    public double Area(double width, double height) { ... }
```
```

# Section 47.8: Access rights

```
```csharp
// static: is callable on a class even when no instance of the class has been created
public static void MyMethod()

// virtual: can be called or overridden in an inherited class
public virtual void MyMethod()

// internal: access is limited within the current assembly
internal void MyMethod()

//private: access is limited only within the same class
private void MyMethod()

//public: access right from every class / assembly
public void MyMethod()

//protected: access is limited to the containing class or types derived from it
protected void MyMethod()

//protected internal: access is limited to the current assembly or types derived from the containing class.
protected internal void MyMethod()
```
```