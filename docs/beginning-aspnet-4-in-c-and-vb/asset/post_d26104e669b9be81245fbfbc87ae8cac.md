
very few times when you need this sort of functionality, but until now, the C# language had no way of accommodating you.

First let's see what the DynamicObject looks like:

```csharp
class WroxDynamicObject : DynamicObject
{
    Dictionary<string, object> _dynamicData = new Dictionary<string, object>();

    public override bool TryGetMember(GetMemberBinder binder, out object result)
    {
        bool success = false;
        result = null;
        if (_dynamicData.ContainsKey(binder.Name))
        {
            result = _dynamicData[binder.Name];
            success = true;
        }
        else
        {
            result = "Property Not Found!";
            success = false;
        }
        return success;
    }

    public override bool TrySetMember(SetMemberBinder binder, object value)
    {
        _dynamicData[binder.Name] = value;
        return true;
    }

    public override bool TryInvokeMember(InvokeMemberBinder binder,
                                          object[] args,
                                          out object result)
    {
        dynamic method = _dynamicData[binder.Name];
        result = method((DateTime)args[0]);
        return result != null;
    }
}
```

code snippet Dynamic\Program.cs

In this example, you're overriding three methods: TrySetMember, TryGetMember, and TryInvokeMember.

TrySetMember adds the new method, property, or field to the object. In this example, you store the member information in a Dictionary object. The SetMemberBinder object that is passed into the TrySetMember method contains the Name property, which is used to identify the element in the Dictionary.

The TryGetMember retrieves the object stored in the Dictionary based on the GetMemberBinder Name property.

So how are these used? Here is the code that makes use of the new dynamic object just created:

```csharp
dynamic wroxDyn = new WroxDynamicObject();
wroxDyn.FirstName = "Bugs";
wroxDyn.LastName = "Bunny";
Console.WriteLine(wroxDyn.GetType());
Console.WriteLine("{0} {1}", wroxDyn.FirstName, wroxDyn.LastName);
```

Looks simple enough, but where is the call to the methods you overrode? Well, that's where the .NET Framework helps. DynamicObject handles the binding for you; all you have to do is reference the properties FirstName and LastName as if they were there all the time.

## SUMMARY

This chapter showed you how the new `dynamic` type can be used. You also saw what the compiler does when it sees a `dynamic` type. The Dynamic Language Runtime was discussed and you were able to host it in a simple app. You used Python as a way to use the DLR, and executed Python scripts, passing in and out values for the scripts to use. And finally, you created your own `dynamic` type by deriving a class from `DynamicObject`.

Dynamic development is becoming very popular. It allows you to do things that are very difficult in a statically typed language. The `dynamic` type and the DLR allow C# programmers to make use of some dynamic capabilities.

## Value Data Types

Windows uses a system known as *virtual addressing*, in which the mapping from the memory address seen by your program to the actual location in hardware memory is entirely managed by Windows. The result of this is that each process on a 32-bit processor sees 4GB of available memory, regardless of how much hardware memory you actually have in your computer (on 64-bit processors this number will be greater). This 4GB of memory contains everything that is part of the program, including the executable code, any DLLs loaded by the code, and the contents of all variables used when the program runs. This 4GB of memory is known as the *virtual address space* or *virtual memory*. For convenience, in this chapter, we call it simply *memory*.

Each memory location in the available 4GB is numbered starting from zero. To access a value stored at a particular location in memory, you need to supply the number that represents that memory location. In any compiled high-level language, including C#, Visual Basic, C++, and Java, the compiler converts human-readable variable names into memory addresses that the processor understands.

Somewhere inside a process's virtual memory is an area known as the *stack*. The stack stores value data types that are not members of objects. In addition, when you call a method, the stack is used to hold a copy of any parameters passed to the method. To understand how the stack works, you need to understand the importance of variable scope in C#. If variable *a* goes into scope before variable *b*, then *b* will always go out of scope first. Look at this code:

```
{
    int a;
    // do something
    {
        int b;
        // do something else
    }
}
```

First, *a* gets declared. Then, inside the inner code block, *b* gets declared. Then the inner code block terminates and *b* goes out of scope, then *a* goes out of scope. So, the lifetime of *b* is entirely contained within the lifetime of *a*. The idea that you always deallocate variables in the reverse order to how you allocate them is crucial to the way the stack works.

You will also notice that *b* is in a different block of code (defined by a different nesting of curly braces). For this reason, it is contained within a different scope. This is termed as *block scope* or *structure scope*.

You do not need to know exactly where in the address space the stack is — you don't need to know for C# development. A *stack pointer* (a variable maintained by the operating system) identifies the next free location on the stack. When your program first starts running, the stack pointer will point to just past the end of the block of memory that is reserved for the stack. The stack actually fills downward, from high memory addresses to low addresses. As data is put on the stack, the stack pointer is adjusted accordingly, so it always points to just past the next free location. This is illustrated in Figure 13-1, which shows a stack pointer with a value of 800000 (0xC3500 in hex); the next free location is the address 799999.

![](img/d7d2ffa0a76feaab821930e95daace93_369_0.png)

FIGURE 13-1

This code assumes the existence of two classes, Customer and EnhancedCustomer. The EnhancedCustomer class extends the Customer class.

First, you declare a Customer reference called arabel. The space for this is allocated on the stack, but remember that this is only a reference, not an actual Customer object. The arabel reference takes up 4 bytes, enough space to hold the address at which a Customer object will be stored. (You need 4 bytes to represent a memory address as an integer value between 0 and 4GB.)

The next line,

```
arabel = new Customer();
```

does several things. First, it allocates memory on the heap to store a Customer object (a real object, not just an address). Then it sets the value of the variable arabel to the address of the memory it has allocated to the new Customer object. (It also calls the appropriate Customer() constructor to initialize the fields in the class instance, but we won't worry about that here.)

The Customer instance is not placed on the stack — it is placed on the heap. In this example, you don't know precisely how many bytes a Customer object occupies, but assume for the sake of argument that it is 32. These 32 bytes contain the instance fields of Customer as well as some information that .NET uses to identify and manage its class instances.

To find a storage location on the heap for the new Customer object, the .NET runtime looks through the heap and grabs the first adjacent, unused block of 32 bytes. Again for the sake of argument, assume that this happens to be at address 200000, and that the arabel reference occupied locations 799996 through 799999 on the stack. This means that before instantiating the arabel object, the memory content will look similar to Figure 13-2.

![](img/d7d2ffa0a76feaab821930e95daace93_371_0.png)

FIGURE 13-2

After allocating the new Customer object, the content of memory will look like Figure 13-3. Note that unlike the stack, memory in the heap is allocated upward, so the free space can be found above the used space.

![](img/d7d2ffa0a76feaab821930e95daace93_371_1.png)

FIGURE 13-3
