object, but its constructor has not finished executing yet! This can be a very hard bug to track down, especially because it is all due to timing.

The call to Volatile.Write fixes this problem. It ensures that the reference in temp can be published into s_value only after the constructor has finished executing. Another way to solve this problem would be to mark the s_value field with C#'s volatile keyword. This makes the write to s_value volatile, and again, the constructor has to finish running before the write can happen. Unfortunately, this makes all reads volatile, too, and because there is no need for this, you are hurting your performance with no benefit.

In the beginning of this section, I mentioned that the double-check locking technique is not that interesting. In my opinion, developers think it is cool, and they use it far more often than they should. In most scenarios, this technique actually hurts efficiency. Here is a much simpler version of the Singleton class that behaves the same as the previous version. This version does not use the double-check locking technique.

```
```csharp
internal sealed class Singleton {
    private static Singleton s_value = new Singleton();

    // Private constructor prevents any code outside this class from creating an instance
    private Singleton() {
        // Code to initialize the one Singleton object goes here...
    }

    // Public, static method that returns the Singleton object (creating it if necessary)
    public static Singleton GetSingleton() { return s_value; }
}
```
```

Because the CLR automatically calls a type's class constructor the first time code attempts to access a member of the class, the first time a thread queries Singleton's GetSingleton method, the CLR will automatically call the class constructor, which creates an instance of the object. Furthermore, the CLR already ensures that calls to a class constructor are thread safe. I explained all of this in Chapter 8. The one downside of this approach is that the type constructor is called when any member of a class is first accessed. If the Singleton type defined some other static members, then the Singleton object would be created when any one of them was accessed. Some people work around this problem by defining nested classes.

Let me show you a third way of producing a single Singleton object.

```
```csharp
internal sealed class Singleton {
    private static Singleton s_value = null;

    // Private constructor prevents any code outside this class from creating an instance
    private Singleton() {
        // Code to initialize the one Singleton object goes here...
    }

    // Public, static method that returns the Singleton object (creating it if necessary)
    public static Singleton GetSingleton() {
        if (s_value != null) return s_value;
```
```