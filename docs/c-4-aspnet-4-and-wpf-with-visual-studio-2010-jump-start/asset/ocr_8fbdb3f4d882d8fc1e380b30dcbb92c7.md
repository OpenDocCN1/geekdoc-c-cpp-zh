```
IL_0057:  ldsfld   class [System.Core]System.Runtime.CompilerServices.CallSite`1
<class [mscorlib]System.Action`1
<class [System.Core]System.Runtime.CompilerServices.CallSite,
class [mscorlib]System.Type,object>> DeCompile.Program/'<Main>$__Site1'
    IL_005c:  ldtoken  [mscorlib]System.Console
IL_0061:  call     class [mscorlib]System.Type [mscorlib]System.Type::GetTypeFromHandle
    (valuetype [mscorlib]System.RuntimeTypeHandle)
IL_0066:  ldloc.0
IL_0067:  ldfld    object DeCompile.DynamicClass::DynValue
IL_006c:  callvirt instance void class [mscorlib]System.Action`3
    <class [System.Core]System.Runtime.CompilerServices.CallSite, class
[mscorlib]System.Type,object>::Invoke(10,11,12)
IL_0071:  nop
IL_0072:  call     string [mscorlib]System.Console::ReadLine()
IL_0077:  pop
IL_0078:  ret
} // end of method Program::Main
```

So it's safe to say that the C# compiler is doing a little extra work to support the dynamic type. Looking at the generated code, you can see references to System.Runtime.CompilerServices.CallSite and System.Runtime.CompilerServices.CallSiteBinder.

The CallSite is a type that handles the lookup at runtime. When a call is made on a dynamic object at runtime, something has to go and look at that object to see if the member really exists. The call site caches this information so the lookup doesn't have to be performed repeatedly. Without this process, performance in looping structures would be questionable.

After the CallSite does the member lookup, the CallSiteBinder is invoked. It takes the information from the call site and generates an expression tree representing the operation the binder is bound to.

There is obviously a lot going on here. Great care has been taken to optimize what would appear to be a very complex operation. It should be obvious that while using the dynamic type can be useful, it does come with a price.

# CODE CONTRACTS

Design-by-contracts is an idea from the Eiffel programming language. Now .NET 4 includes classes for static and runtime checks of code within the namespace System.Diagnostics.Contracts that can be used by all .NET languages.

With this functionality you can define preconditions, postconditions, and invariants within a method. The preconditions lists what requirements the parameters must fulfill, the postconditions define the requirements on returned data, and the invariants define the requirements of variables within the method itself.

Contract information can be compiled both into the debug and the release code. It is also possible to define a separate contract assembly, and many checks can also be made statically without running the application. You can also define contracts on interfaces that cause the implementations of the interface to fulfill the contracts. Contract tools can rewrite the assembly to inject contract checks