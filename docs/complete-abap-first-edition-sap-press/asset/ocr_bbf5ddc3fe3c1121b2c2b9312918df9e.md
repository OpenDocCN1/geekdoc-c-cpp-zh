+   - `CX_DYNAMIC_CHECK`
+     Similar to `CX_STATIC_CHECK`, if an exception class that's a subclass of `CX_DYNAMIC_CHECK` is raised in a function module or method, it should either be defined in the signature (parameter interface) or caught in the procedure within a `TRY` block. Otherwise, the compiler will not give a static warning message statically but will produce a runtime error.

+   - `CX_NO_CHECK`
+     The exception class that is a subclass of `CX_NO_CHECK` can't be defined in the signature of a function module or method. It's implicitly declared by default and always propagated to the caller.

Because `CX_STATIC_CHECK` is checked by the compiler during design time, it's recommended to use this class to define exception classes. Most system exceptions are derived from `CX_DYNAMIC_CHECK`.

SAP has implemented many exception classes that can be used out of the box. The keyword documentation lists all the available system exception classes, as shown in Figure 9.13. Keyword documentation can be accessed using Transaction ABAP-DOCU.

![](bbox=[0.142, 0.503, 0.713, 0.867])

Figure 9.13  System Exception Classes in Keyword Documentation