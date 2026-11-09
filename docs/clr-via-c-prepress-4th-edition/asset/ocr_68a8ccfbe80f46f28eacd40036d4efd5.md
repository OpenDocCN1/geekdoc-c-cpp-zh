```
```csharp
#if INEFFICIENT
                // When compiling the following line, v is boxed
                // three times, wasting time and memory.
                Console.WriteLine("{0}, {1}, {2}", v, v, v);
#else
                // The lines below have the same result, execute
                // much faster, and use less memory.
                Object o = v; // Manually box v (just once).

                // No boxing occurs to compile the following line.
                Console.WriteLine("{0}, {1}, {2}", o, o, o);
#endif
            }
        }
```
```

If the code is compiled with the INEFFICIENT symbol defined, the compiler will generate code to box v three times, causing three objects to be allocated from the heap! This is extremely wasteful since each object will have exactly the same contents: 5. If the code is compiled without the INEFFICIENT symbol defined, v is boxed just once, so only one object is allocated from the heap. Then, in the call to Console.WriteLine, the reference to the single boxed object is passed three times. This second version executes much faster and allocates less memory from the heap.

In these examples, it’s fairly easy to recognize when an instance of a value type requires boxing. Basically, if you want a reference to an instance of a value type, the instance must be boxed. Usually this happens because you have a value type instance and you want to pass it to a method that requires a reference type. However, this situation isn’t the only one in which you’ll need to box an instance of a value type.

Recall that unboxed value types are lighter-weight types than reference types for two reasons:

+   - They are not allocated on the managed heap.
+   - They don’t have the additional overhead members that every object on the heap has: a type object pointer and a sync block index.

Because unboxed value types don’t have a sync block index, you can’t have multiple threads synchronize their access to the instance by using the methods of the System.Threading.Monitor type (or by using C#’s lock statement).

Even though unboxed value types don’t have a type object pointer, you can still call virtual methods (such as Equals, GetHashCode, or ToString) inherited or overridden by the type. If your value type overrides one of the virtual methods, then the CLR can invoke the method nonvirtually because value types are implicitly sealed and cannot have any types derived from them. In addition, the value type instance being used to invoke the virtual method is not boxed. However, if your override of the virtual method calls into the base type's implementation of the method, then the value type instance does get boxed when calling the base type's implementation so that a reference to a heap object get passed to the this pointer into the base method.

However, calling a nonvirtual inherited method (such as GetType or MemberwiseClone) always