
were to call a value type's virtual method virtually, the CLR would need to have a reference to the value type's type object in order to refer to the method table within. This requires boxing the value type. Boxing puts pressure on the heap, forcing more frequent garbage collections and hurting performance.

Regardless of whether or callvirt is used to call an instance or virtual method, these methods always receive a hidden argument as the method's first parameter. This argument refers to the object being operated on.

When designing a type, you should try to minimize the number of virtual methods you define. First, calling a virtual method is slower than calling a nonvirtual method. Second, virtual methods cannot be inlined by the JIT compiler, which further hurts performance. Third, virtual methods make versioning of components more brittle, as described in the next section. Fourth, when defining a base type, it is common to offer a set of convenience overloads. If you use these methods to be polymorphic, the best thing to do is to make the most complex method virtual and leave all of the convenience methods nonvirtual. By the way, following this guideline will also improve the ability to verify a component without adversely affecting the derived types. Here is an example.

```cs
public class Set {
    private Int32 m_length = 0;
    // convenience overload is not virtual
    public Int32 Find(Object value) {
        return Find(value, 0, m_length);
    }

    // convenience overload is not virtual
    public Int32 Find(Object value, Int32 startIndex) {
        return Find(value, startIndex, m_length - startIndex);
    }

    // The feature-rich method is virtual and can be overridden
    public virtual Int32 Find(Object value, Int32 startIndex, Int32 endIndex) {
        // Actual implementation that can be overridden here...
    }

    // Other methods go here
}
```

## Using Visibility and Member Accessibility Intelligently

With the .NET Framework, applications are composed of types defined in multiple assemblies produced by various companies. This means that the developer has little control over the components he or she is using and the types defined within those components. The developer typically doesn't have access to the source code (and probably doesn't even know what programming language was used to create the component), and components tend to version with different schedules. Furthermore, due to polymorphism and protected members, a base class developer must trust the code written by the derived class developer. And, of course, the developer of a derived class must trust the code that he is inheriting from a base class. These are some of the issues that you need to really think about when designing components and types.

In this section, I'd like to just say a few words about how to design a type with these issues in mind. Specifically, I'm going to focus on the proper way to set type visibility and member accessibility that you'll be most successful.

First, when defining a new type, compilers should make the sealed class default so that the class cannot be used as a base class. Instead, many compilers, including C#, default to sealed classes and allow the programmer to explicitly mark a class as sealed using the sealed keyword. Obviously, it is too late now, but I think today's compilers have chosen the wrong default and it would benefit if this changed with future compilers. There are three reasons why a sealed class is better than an unsealed class:

- **Versioning**: When a class is originally sealed, it can change to sealed in the future without breaking compatibility. However, after a class is unsealed, you can never change it to sealed in the future as this would break all classes. In addition, if the unsealed class defines any virtual methods, ordering of the virtual calls must be maintained with new versions or there is the potential of breaking types in the future.

- **Performance**: As discussed in the previous section, calling a virtual method doesn't perform as well as calling a nonvirtual method because the CLR must look up the type of the object at run time to determine which type defines the method to call. However, if the JIT compiler calls a virtual method using a sealed type, the JIT compiler can produce more efficient code by calling the method nonvirtually. It can do this because it knows can't possibly be a derived class if the class is sealed. For example, in the code below, the JIT compiler can call the virtual ToString nonvirtually.

```cs
using System;
public sealed class Point {
    private Int32 x, y;

    public Point(Int32 x, Int32 y) { m_x = x; m_y = y; }

    public override string ToString() {
        return String.Format("{0}, {1}", m_x, m_y);
    }

    public static void Main() {
        Point p = new Point(3, 4);
        // The C# compiler emits the callvirt instruction here
        // The JIT compiler will optimize this call and produce code that
        // calls ToString nonvirtually because p's type is Point,
        // which is a sealed class
        Console.WriteLine(p.ToString());
    }
}
```

- **Security and predictability**: A class must protect its own state and not allow it ever become corrupted. When a class is unsealed, a derived class can access and manipulate the base class's state if any data fields or methods that internally manipulate fields are accessible and not private. In addition, a virtual method can be overridden by a derived class, and the derived class can decide whether to call the base class's implementation. By making a method, property, or event virtual, the base class gives up control over its behavior and its state. Unless carefully thought out, this can cause the object to behave unpredictably, and open potential security holes.

The problem with a sealed class is that it can be a big inconvenience to users of the type. Occasionally, developers want to create a derived class from an existing type in order to attach some fields or state. In fact, they may want to define some helper methods on the derived type. Although the CLR offers no mechanism to extend an already-built type with helper methods, you can simulate methods using C# extension methods (discussed in Chapter 8) and simulate state onto an object using ConditionalWeakTable. Here are the guidelines I follow when I define my classes:

- When defining a class, I explicitly make it sealed unless I intend for it to be a base class that allows specialization by derived classes. As stated earlier, this is the opposite of what C# and many other compilers default to. I also default to making the class internal unless I want the class to be public outside of my assembly. Frequently, if you do not explicitly indicate a type's visibility, the C# compiler defaults to internal. If it is important to define a class that others can derive but I do not want to allow specialization, I will simulate creating a closed class by using the above technique of sealing the virtual methods that my class inherits.

- Inside the class, I define my fields as private and never waive on them. Fortunately, C# defaults to making fields private. I would actually prefer it to be C# mandated that all fields be private and that you could not make fields protected, internal, public, and so on. Exposing state is the easiest way to get into problems, have your object behave unpredictably, and open potential security holes. This is true if you declare some fields as internal. Even within a single assembly, it is too hard to track back all code that references a field.

- Inside the class, I define my methods, properties, and events as private and nonvirtual. Fortunately, C# defaults to this as well. Certainly, I would make a method, property, or event public to expose some functionality from the type. I try to avoid making any of these members protected or internal because this would be exposing my type to some potential vulnerability. However, I sooner make a member protected or internal than I would make a member virtual because a virtual member gives up control and really relies on the proper behavior of the derived class.
