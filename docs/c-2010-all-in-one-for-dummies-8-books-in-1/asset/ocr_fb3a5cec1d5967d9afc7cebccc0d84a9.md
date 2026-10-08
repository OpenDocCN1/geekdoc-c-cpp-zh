Programs throughout this book make items in NamespaceB visible in NamespaceA with the using directive. I discuss full qualification and using directives in the next two sections.

If the items in NamespaceB are in other assemblies, choose Project::+ Add Reference and add a reference for those assemblies.

![](bbox=[0.123, 0.187, 0.193, 0.252])

# Using fully qualified names

The namespace of a class is a part of the extended class name, which leads to the first way to make classes in one namespace visible in another. This example does not using any directives to simplify referring to classes in other namespaces:

```
namespace MathRoutines // Broken into two segments -- see below.
class Sort {
    public void SomeMethod() {
}
namespace Paint {
    public class PaintColor{
        public PaintColor(int nRed, int nGreen, int nBlue ()) {}
        public void Paint() {}
        public static void StaticPaint() {}
    }
}
namespace MathRoutines // Another piece of this namespace
class Test {
    public static void main(string[] args) {
        // Create an object of type Sort from the same namespace
        // we're in and invoke a method.
        Sort obj = new Sort();
        obj.SomeMethod();
        // Create an object in another namespace -- notice that the
        // namespace name must be included explicitly in every
        // class reference.
        Paint.PaintColor black = new Paint.PaintColor(0, 0, 0);
        black.Paint();
        Paint.PaintColor.StaticPaint();
    }
}
```

In this case, the classes Sort and Test are contained within the different namespace, MathRoutines, even though they appear in the different declarations within the file (or different files). That namespace is broken into two parts.