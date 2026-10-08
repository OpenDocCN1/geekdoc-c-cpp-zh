
class can perform and what information the class makes publicly available. As long as the public interface does not change, the internal details can change in any way required without having an adverse effect on other classes or code that depends on it.

By keeping the public interface of a class small and by providing a high degree of fidelity between your class and the real-world object it represents, you help ensure that your class will be familiar to other programmers who need to use it.

Let's look at our car example again. By encapsulating the details of what happens when you start your car and providing an action, `StartCar`, and information, such as `IsCarStarted`, we have defined a public interface, thereby creating an abstraction (or at least a partial abstraction, because cars do much more than just start) of a car.

## Component-Oriented Programming

Component-oriented programming is a technique of developing software applications by combining pre-existing and new components, much the same way automobiles are built from other components. Software components are self-contained, self-describing packages of functionality containing definitions of types that expose both behavior and data.

C# supports component-oriented programming through the concepts of properties, methods, events, and attributes (or metadata), allowing self-contained and self-describing components of functionality called assemblies.

## Classes in C#

Now that you have a basic understanding of object-oriented and component-oriented programming, it is time to see how C# enables these concepts to become reality by using classes. You have actually already used classes in the examples and exercises from the previous two hours.

Classes in C# are reference types that implicitly derive from `object`. To define a class, you use the `class` keyword. Look at the application you built at the end of Hour 1, “The .NET Framework and C#.” Everything you did was inside a class named `Program`.

The `body` of the class, defined by the opening and closing braces, is where you define the data and behavior for the class.

## Scope and Declaration Space

We briefly mentioned scope and declaration space in Hour 1, saying that scope defines where you can use a name, whereas declaration space focuses on where that name is unique. Scope and declaration space are closely related, but there are a few subtle differences.

A more formal definition is that scope is an enclosing context or region that defines where a name can be used without qualification.

In C#, both scope and declaration space is defined by a statement block enclosed by braces. That means namespaces, classes, methods, and properties all define both a scope and a declaration space. As a result, scopes can be nested and overlap each other.

If scope defines the visibility of a name and scopes are allowed to overlap, any name defined in an outer scope is visible to an inner scope, but not the other way around.

In the code shown in Listing 3.1, the field age is in scope throughout the entire body of Contract, including within the body of F and G. In F, the use of age refers to the field named age.

**LISTING 3.1   Scope and Declaration Space**

```
class Contract
{
   public int age;

   public void F()
   {
      age = 18;
   }

   public void G()
   {
      int age;
      age = 21;
   }
}
```

However, in G, the scopes overlap because there is also a local variable named age that is in scope throughout the body of G. Within the scope of G, when you refer to age, you are actually referring to the locally scoped entity named age and not the one in the outer scope. When this happens, the name declared in the outer scope is hidden by the inner scope.

Figure 3.1 shows the same code with the scope boundaries indicated by the dotted and dashed rectangles.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_87_0.png)

**FIGURE 3.1  
Nested scopes and hiding**

Declaration space, on the other hand, is an enclosing context or region in which no two entities are allowed to have the same name. In the Contact class, for example, you are not allowed to have anything else named *age* in the body of the class, excluding the bodies of *F* and *G*. Likewise, inside the body of *G*, when you redeclare *age*, you aren’t allowed to have anything else named *age* inside the declaration space of *G*.

You learn about method overloading a bit later this hour, but methods are treated a little differently when it comes to declaration spaces. If you consider the set of all overloaded methods with the same name as a single entity, the rule of having a unique name inside a declaration space is still satisfied.

## Try It Yourself

### Working with Scope

To explore the differences between scope and declaration space, follow these steps. Keep Visual Studio open at the end of this exercise because you will use this application later.

- 1. Create a new Console application.
- 2. Add a new class file named `Contact.cs` that looks like Listing 3.1.
- 3. In G, add a `Console.WriteLine` statement at the end of the method that prints the value of *age*.
- 4. In the Main method of the Program.cs file, enter the following code to create a new instance of the Contact class and print the current value of age:

```
Contact c = new Contact();
Console.WriteLine(c.age);
c.F();
Console.WriteLine(c.age);
G();
Console.WriteLine(c.age);
```

- 5. Run the application using Ctrl+F5 and observe that the output matches what is shown in Figure 3.2.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_88_0.png)

## Accessibility

Accessibility enables you to control the visibility, or accessibility, of an entity outside of its containing scope. C# provides this through access modifiers, which specify constraints on how members can be accessed outside the boundary of the class and, in some cases, even constrain inheritance. A particular class member is accessible when access to that member has been allowed; conversely, the member is inaccessible when access has been disallowed.

These access modifiers follow a simple set of contextual rules that determine when certain types of accessibility are permitted:

- Namespaces are not allowed to have any access modifiers and are always public.
- Classes default to internal accessibility but are allowed to have either public or internal declared accessibility. A nested class, which is a class defined inside of another class, defaults to private accessibility but can have any of the five kinds of declared accessibility.
- Class members default to private accessibility but can have any of the five kinds of declared accessibility.

These rules also define the default accessibility, which occurs when a member does not include any access modifiers.

## Explicitly Declaring Accessibility

Although C# provides reasonable default access modifiers, you should always explicitly declare the accessibility of your class members. This prevents unintended ambiguity, indicates that the choice was a conscious decision, and is self-documenting.

The access modifiers supported by C# are shown in Table 3.1.

**TABLE 3.1  Access Modifiers**

| Modifier | Description |
| :--- | :--- |
| public | Access is not limited. |
| protected | Access is limited to the containing class or types derived from the containing class. |
| internal | Access is limited to the containing assembly. |
| protected internal | Access is limited to the containing assembly or types derived from the containing class. |
| private | Access is limited to the containing class only. |

## Protected Internal

Be careful when using protected internal accessibility because it is effectively protected or internal. C# does not provide a concept of protected and internal.

## Fields and Constants

Fields are variables that represent data associated with a class. In other words, a field is simply a variable defined in the outermost scope of a class. If you recall from Hour 1, a field can be either an instance field or a static field, and for both types of field, you can specify any of the five access modifiers. Typically, fields are private, which is the default.

If a field, no matter whether it is an instance or static field, is not given an initial value when it is declared, it is assigned the default value appropriate for its type.

Similar to fields, constants can be declared with the same access modifiers. Because a constant must have a value that can be computed at compile time, it must be assigned a value as part of its declaration. One benefit of requiring a value that can be computed at compile time is that a constant can depend on other constants.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_89_0.png)

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_89_1.png)
