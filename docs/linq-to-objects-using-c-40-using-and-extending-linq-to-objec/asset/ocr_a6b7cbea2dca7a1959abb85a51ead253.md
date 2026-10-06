# DYNAMIC TYPING 245

the new dynamic type from the System.Dynamic.DynamicObject type supplied to make this easier.

Any traditional type of object can be declared as type dynamic. For all dynamic objects that do not implement the interface IDynamicMetaObjectProvider, the Microsoft.CSharp.RuntimeBinder is employed to look up property and method invocations at runtime. The example code shown in Figure 8-1 shows the Intellisense balloon in an attempt to declare an integer type declared as dynamic. (The runtime resolves the type by the initialization expression, just like the local type inference var keyword.) No compile error occurs at design time or compile time, even though the method call is not defined anywhere in the project. When this code is executed, the runtime uses reflection in an attempt to find and execute the fictitious method MethodNotDefinedAnywhere, which of course fails with the exception:

Microsoft.CSharp.RuntimeBinder.RuntimeBinderException: 'int' does not contain a definition for 'MethodNotDefinedAnywhere'

```
dynamic o = 1;
o.MethodNotDefinedAnywhere();
dynamic.expression
This operation will be resolved at runtime
```

FIGURE 8-1 Any object declared as type dynamic is resolved at runtime. No errors will be reported at compile time.

If that method had been actually declared, it would have been simply invoked just like any traditional method or property call.

The ability to have a type that doesn't implement the IDynamicObject interface should be rare. The dynamic keyword shouldn't be used in place of a proper type definition when type is known at compile time. It also shouldn't be used in place of the var keyword when working with anonymous types, as that type is known at compile time. The dynamic keyword should only be used to declare IDynamicMetaObjectProvider implementers and for interoperating with other dynamic languages and for COM-Interop.