method attribute-target-specifier indicates that the attribute applies to the method; the presence of the return attribute-target-specifier indicates that the attribute applies to the return value.

+   - An attribute specified on an operator declaration can apply either to the operator being declared or to its return value. In the absence of an attribute-target-specifier, the attribute applies to the operator. The presence of the method attribute-target-specifier indicates that the attribute applies to the operator; the presence of the return attribute-target-specifier indicates that the attribute applies to the return value.
+   - An attribute specified on an event declaration that omits event accessors can apply to the event being declared, to the associated field (if the event is not abstract), or to the associated add and remove methods. In the absence of an attribute-target-specifier, the attribute applies to the event. The presence of the event attribute-target-specifier indicates that the attribute applies to the event; the presence of the field attribute-target-specifier indicates that the attribute applies to the field; and the presence of the method attribute-target-specifier indicates that the attribute applies to the methods.
+   - An attribute specified on a get accessor declaration for a property or indexer declaration can apply either to the associated method or to its return value. In the absence of an attribute-target-specifier, the attribute applies to the method. The presence of the method attribute-target-specifier indicates that the attribute applies to the method; the presence of the return attribute-target-specifier indicates that the attribute applies to the return value.
+   - An attribute specified on a set accessor declaration for a property or indexer declaration can apply either to the associated method or to its lone implicit parameter. In the absence of an attribute-target-specifier, the attribute applies to the method. The presence of the method attribute-target-specifier indicates that the attribute applies to the method; the presence of the param attribute-target-specifier indicates that the attribute applies to the parameter; the presence of the return attribute-target-specifier indicates that the attribute applies to the return value.
+   - An attribute specified on an add or remove accessor declaration for an event declaration can apply either to the associated method or to its lone parameter. In the absence of an attribute-target-specifier, the attribute applies to the method. The presence of the method attribute-target-specifier indicates that the attribute applies to the method; the presence of the param attribute-target-specifier indicates that the attribute applies to the parameter; the presence of the return attribute-target-specifier indicates that the attribute applies to the return value.

In other contexts, inclusion of an attribute-target-specifier is permitted but unnecessary. For instance, a class declaration may either include or omit the specifier type:

```
[type: Author("Brian Kernighan")]
class Class1 {}
[Author("Dennis Ritchie")]
class Class2 {}
```

It is an error to specify an invalid attribute-target-specifier. For instance, the specifier param cannot be used on a class declaration:

```
[param: Author("Brian Kernighan")]    // Error
class Class1 {}
```

By convention, attribute classes are named with a suffix of Attribute. An attribute-name of the form type-name may either include or omit this suffix. If an attribute class is found both with and without this suffix, an ambiguity is present, and a compile-time error results. If the attribute-name is spelled such that its right-most identifier is a verbatim identifier (§2.4.2), then only an attribute without a suffix is matched, thus enabling such an ambiguity to be resolved. The example

```
using System;
```