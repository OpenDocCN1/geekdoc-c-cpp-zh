# Example B.39.

```
class Appendix_B {
    static void Main() {
        long Number;
    }
}
```

# namespace

When we encompass our coding inside a namespace, we are actually declaring a scope or globally unique partition. The types contained in that namespace are accessible through direct access (from within that body), and through the using-namespace-directive, which allows us to use its values without qualification (see Example B.40)

# Example B.40.

```
namespace Appendix_B {
    class Class1 {
        static void Main() {}
    }
}
```

# new

The keyword new is used as both an operator and a modifier. As an operator, it is used to declare instances and to create objects. As a modifier, it is used to hide members inherited from a base class. Note that the new operator cannot be overloaded, nor can it be used with the override statement (see Example B.41).

# Example B.41.

```
namespace Appendix_B {
    public class BaseClass {
        public short x;
        protected BaseClass() {}
        public short X {set{x = value;}}
    }

    public class DerivedClass : BaseClass {
        protected DerivedClass() {}
```