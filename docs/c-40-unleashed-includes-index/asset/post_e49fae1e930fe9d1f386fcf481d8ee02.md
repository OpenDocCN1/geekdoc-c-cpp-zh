
One common question concerns debugging of dynamic objects. In environments where static typing is the standard, you can simply see the object's members while carrying out debugging tasks. Fear not, as the GetDynamicMemberNames method is there for you to override to provide debugging information:

```
public override IEnumerable<string> GetDynamicMemberNames()
{
    return _bag.Keys;
}
```

Visual Studio 2010 has been enlightened about objects that can provide a dynamic list of member names, as shown in Figure 22.19. When expanding the list of members, a call is made to the preceding method, followed by a series of calls to gain access to the value of those members. Talking about debugging, it's even possible to use the Immediate Window to perform dynamic operations. Because of those features, debugging dynamically typed code is relatively easy.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1173_0.png)

FIGURE 22.19 Some debugging features with support for C# 4.0 dynamic.

## A Primer to DynamicMetaObject

As you saw earlier, the use of DynamicObject allows an object to participate in the binding process for a wide variety of operations. This is actually aligned with a general design philosophy in the DLR where objects get the first crack at defining meaning for binding operations, before language-specific binders get around to assist.

One of the core benefits of such dynamic objects is they follow a protocol that allows them to be used across different languages. Our self-written Bag object can therefore be used from languages other than C# (for example, from IronPython, as shown in Figure 22.20).

This common protocol for interoperability with dynamic objects lives at a level lower than the DynamicObject base type, though. Here the IDynamicMetaObjectProvider interface and the auxiliary DynamicMetaObject type enter the picture. The definition of those two types is shown in Figure 22.21.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1174_0.png)

FIGURE 22.20 Using our Bag dynamic object in IronPython.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1174_1.png)

FIGURE 22.21 Types at the heart of dynamic object interoperability.

One of the key differences between DynamicObject and DynamicMetaObject is the difference in the signature of Bind operations, which correspond to the family of Try methods in DynamicObject. Although those methods are also passed a Binder object, their arguments and return types use DynamicMetaObject objects.

The essential piece of information contained by a DynamicMetaObject instance is an expression tree that represents the code that has to be executed to compute its value. It's the DLR's role to stitch together such expression trees to make up efficient call sites that can get compiled into IL code at runtime. This is the place where the object is in total control to define the semantics of the operation that will produce its value, which enables it to emit highly efficient code.

Besides the expression tree kept in the Expression property, a DynamicMetaObject can also have a set of binding restrictions that determine when binding to the object is permitted. Such restrictions can be based on types, be written as an expression tree that will carry out some check, or restrict validity for binding to a particular instance.

When we looked at call sites earlier, in this chapter's “Dynamic Call Sites and Binders” section, we saw that the code emitted for dynamic dispatch sites have the following form:

```
(CallSite site, object a, object b) =>
{
    if (a is int && b is int)
        return (int)a + (int)b;
    if (a is DateTime && b is TimeSpan)
        return (DateTime)a + (TimeSpan)b;
    return site.Update(site, a, b);
}
```

Recall that the way this code got generated is based on the interaction between the binders and the DLR. Once a pair of two Int32 values was encountered for a and b, the DLR handed over the request to the C# runtime binder. If there would have been dynamic objects (checked based on IDynamicMetaObjectProvider), the request would have been handed over to the overridden BindBinaryOperation method. Figure 22.22 shows the relationship between binding restrictions and generated branch instructions.

```
public class DynamicMetaObject
{
    public BindingRestrictions Restrictions { get; }
    public Expression Expression { get; }
    ...
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1175_0.png)

FIGURE 22.22 How restrictions and expressions relate to call sites.

No matter what path was followed, under the covers this interoperability protocol is followed, handing binding restrictions and expressions back to the DLR. In the case of the C# runtime library helping out, it gave us binding restrictions and an expression to compute the value back.

Given this information, the DLR can follow different strategies to optimize call sites, which are known as different cache levels. We don't discuss those implementation details in detail and instead defer to DLR documentation at dlr.codeplex.com. Suffice to say, manual implementation of DynamicMetaObject types will result in great flexibility on the code that gets run when a dynamic operation is carried out.

One example of the use of efficient code generation is caching of result values that rarely change. Immutable types form an extreme of this, where get member operations (and even instance methods that compute values based on the immutable data kept in the object) can be reduced to returning constant values. Although the first hit to operations on the object can take a while to compute the result value, immutability guarantees it won't ever change, so the emitted expression tree can simply return a constant.

Elsewhere on the mutability spectrum are objects that rarely change. For them, the same caching trick can be applied but in combination with some invalidation logic. To make this work, the BindSetMember override would set some flag associated with the member's name to indicate the value has been invalidated. Code emitted for the BindGetMember will include a check for the invalidation flag. Depending on its value, the constant-returning expression will be restricted for use. When the flag is set, a path will be triggered that recomputes the value.

## Dynamic Operations

To finish off our overview of DynamicObject and DynamicMetaObject, we'll take a quick look at the various operations that can be specialized by overriding a method on those base classes. Some of those operations have a C# notation, whereas others exist in dynamic languages only.

- Binary operations, such as mathematical logical operators and (in)equality operators. For example, a + b, a > b, a && b.
- Unary operations, such as logical negation or complement or numeric minus or plus. For example, -a, !a.
- Getting and setting members, which correspond to properties or fields in CLR terms. For example, a.Foo or a.Bar = 5.
- Getting and setting indexes to index into objects such as collections, vectors, and so on. For example, a[0] or vector["x*"] = 1.
- Conversion of objects to some specified type, either explicitly (as with cast syntax) or implicitly. For example, (Hashtable)bag.
- Invocation of members, which correspond to methods in the CLR terms (for example, a.Print("Hello")). Method call syntax in C# maps to this operation. In some dynamic languages, there's no such thing as invoking members, but instead all “methods” are encoded as gettable members that contain a function object. To invoke those, the direct invocation operation is used, as explained next.
- Direct invocation on objects is similar to delegate invocation in C#. For example, a(42). First-class dynamic functions can be driven by this operation.
- Creating instances in a dynamic fashion is not directly supported in C# but is in various dynamic languages. For example, dynamic new Bag.
- Deleting members and indexes is another operation that lacks some syntactic surface in C# but has been around in dynamic languages for a while. For example, in Python, you would write del bag.Name.

For example, to handle the delete member operation, you could extend our Bag dynamic object with an override for TryDeleteMember:

```
public override bool TryDeleteMember(DeleteMemberBinder binder)
{
    return _bag.Remove(binder.Name);
}
```

To show this specialized operation in action, we can use the IronPython console once more and even get into debugging by attaching the debugger to the ipy.exe process. After starting the REPL loop, go to Tools, Attach to Process in Visual Studio 2010 and set a breakpoint on the TryDeleteMember method. Now enter the following code in IronPython:

```
import sys
sys.path.append(r"c:\temp")              #wherever the Bag assembly lives

import clr
clr.AddReferenceToFile("CS40Dynamic.exe") #whatever the Bag assembly file is
from CS40Dynamic import *                  #the namespace containing Bag

person = Bag()
person.Name = "Lisa"
del person.Name
```

Figure 22.23 shows the debugger hit the breakpoint as soon as we use Python's del keyword to delete a member. This illustrates the power of the DLR to unify dynamic objects and dynamic operations in a cross-language manner.

## Overall Architecture

To wrap up our discussion of DLR internals, let's look at an overview diagram of the infrastructure available. Figure 22.24 illustrates the DLR in the middle between languages that are enabled for dynamic and target object domains.
