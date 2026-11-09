In the Main method, a Manager object is constructed and passed to PromoteEmployee. This code compiles and executes because Manager is ultimately derived from Object, which is what PromoteEmployee expects. Once inside PromoteEmployee, the CLR confirms that o refers to an object that is either an Employee or a type that is derived from Employee. Because Manager is derived from Employee, the CLR performs the cast and allows PromoteEmployee to continue executing.

After PromoteEmployee returns, Main constructs a DateTime object and passes it to PromoteEmployee. Again, DateTime is derived from Object, and the compiler compiles the code that calls PromoteEmployee with no problem. However, inside PromoteEmployee, the CLR checks the cast and detects that o refers to a DateTime object and is therefore not an Employee or any type derived from Employee. At this point, the CLR can’t allow the cast and throws a System.InvalidCastException.

If the CLR allowed the cast, there would be no type safety, and the results would be unpredictable, including the possibility of application crashes and security breaches caused by the ability of types to easily spoof other types. Type spoofing is the cause of many security breaches and compromises an application’s stability and robustness. Type safety is therefore an extremely important part of the CLR.

By the way, the proper way to declare the PromoteEmployee method would be to specify an Employee type instead of an Object type as its parameter so that the compiler produces a compile-time error, saving the developer from waiting until a runtime exception occurs to discover a problem. I used Object so that I could demonstrate how the C# compiler and the CLR deal with casting and type-safety.

# ## Casting with the C# is and as Operators

Another way to cast in the C# language is to use the is operator. The is operator checks whether an object is compatible with a given type, and the result of the evaluation is a Boolean: true or false. The is operator will never throw an exception. The following code demonstrates.

```
```csharp
Object o = new Object();
Boolean b1 = (o is Object);   // b1 is true.
Boolean b2 = (o is Employee); // b2 is false.
```
```

If the object reference is null, the is operator always returns false because there is no object available to check its type.

The is operator is typically used as follows.

```
```csharp
if (o is Employee) {
    Employee e = (Employee) o;
    // Use e within the remainder of the 'if' statement.
}
```
```