Compared to C#, there is little difference in the approach for invoking .NET method in F#. Here’s how to use a .NET method to convert a string to an integer:

```
System.Convert.ToInt32("234")
```

Passing a tuple to a C# function seems well until you have a function that requires an out parameter. Tuples do not provide a way to say that a value is ref or out, but a tuple does help to solve this problem. If you have a C# function(int k, out int n)

```
public int CSharpFunction(int k, out int n)
```

the function actually returns two values to the invoker. So the solution is to declare a tuple to hold the returned values:

```
let returnValue, nValue = CSharpFunction(1)
```

This approach works for the method, which is not externally declared. A call to an externally declared method requires the & operator. Listing 1-84 shows how to handle an out parameter in an extern function.

**LISTING 1-84** Using F# to expose a C# extern function that has an out parameter

```
C# function definition
[DllImport("MyDLL.dll")
public static extern int ASSystemFunction(IntPtr inRef, out IntPtrPtr);
Define and invoke the function in F#n[System.Runtime.InteropServices.DllImport("something.dll")]
extern int ASSystemFunction(System.IntPtr inRef, System.IntPtr outPtr);
let mutable myOutPtr = nativeint 1\let n = ASSystemFunction(nativeint 0, &myOutPtr)
```

If you want to expose an out parameter to a C# project, you need a special attribute named System.Runtime.InteropServices.Out. By decorating a parameter with this attribute in F#, the C# invoker can see that the parameter is intended to be an out parameter. See the sample in Listing 1-85. The byref keyword is used to declare the variable as passed in as a reference type.

**LISTING 1-85** Using F# to expose an out parameter to C#

```
let f ([-System.Runtime.InteropServices.Out]:a: byref) = a - 9
```

I covered the out parameter, so now let's shift our attention to ref. It’s easy to handle the C# ref definition well. Listing 1-86 shows how to handle ref parameters in F#. There is a byref keyword in