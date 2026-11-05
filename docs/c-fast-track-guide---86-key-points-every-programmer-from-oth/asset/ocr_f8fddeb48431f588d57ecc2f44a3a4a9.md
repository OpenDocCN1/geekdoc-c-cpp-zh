```
static void Main()
{
// Animal a = new Animal(); // ❌ Error! Cannot instantiate abstract class
Dog myDog = new Dog(); // ✅ Valid
myDog.Breathe(); // Inherited method
myDog.MakeSound(); // Implemented method
}
}
```

# [Execution Result]

Breathing...
Bark!

Abstract classes are used when multiple classes share common logic but differ in implementation of certain behaviors.

Key Points:

+   - You cannot create an instance of an abstract class.
+   - You can define methods with logic in abstract classes (called concrete methods).
+   - You must override abstract methods in derived classes.
+   - It enforces a contract while allowing shared code to prevent duplication.
+   - This is especially useful in real-world applications like game engines or UI systems, where base behaviors are consistent across many entities (e.g., all UI elements can "Draw", but each one draws differently).

# [Supplement]