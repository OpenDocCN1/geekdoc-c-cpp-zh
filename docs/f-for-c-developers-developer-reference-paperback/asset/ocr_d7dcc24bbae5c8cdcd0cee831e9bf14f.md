As a C# developer, you might use the **new** keyword everywhere through force of habit. If that is the case, you should be aware of a small catch when using the new keyword with generic types, the type parameter is automatically set to System.Object in Listing 2-38 to narrow the scope of the code shown below. Also, the type parameter cannot be ignored if you use the new keyword, even if your type parameter is System.Object. See Listing 2-38.

**Listing 2-38** Using the new keyword with a generic type

```
let f () =
  let myDictionary = System.Collections.Generic.List()
  printfn "my type is %A" (myDictionary.GetType())

  // following code does not compile because it needs the type parameter
  let myDictionary2 = new System.Collections.Generic.List()
  printfn "my type is %A" (myDictionary2.GetType())

  let myDictionary2 = new System.Collections.Generic.List<int>()
  printfn "my type is %A" (myDictionary2.GetType())

f()
```

Execution result
my type is System.Collections.Generic.List`1[System.Object]
my type is System.Collections.Generic.List`1[System.Int32]

> Note Creating a generic type without specifying the type parameter does not always work at the top level.

# Using Type Casting

I've already introduced many data types, including both basic types and complex class types. Let me now leave the C# code conversion task and introduce type casting. In a real-world application, you might need to do casting, which could involve not only basic data types, from *int* to *float*, but also object casting up and down the class hierarchy.

# Converting Numbers and Using **enum**

Let's start with a basic type of conversion: *number conversion*. The way F# converts a number is similar to the way that C# does it. See Listing 2-39.