![](bbox=[0.08, 0.12, 0.62, 0.36])

FIGURE 22.20 Using our Bag dynamic object in IronPython.

![](bbox=[0.06, 0.47, 0.62, 0.78])

FIGURE 22.21 Types at the heart of dynamic object interoperability.

One of the key differences between DynamicObject and DynamicMetaObject is the difference in the signature of Bind operations, which correspond to the family of Try methods in DynamicObject. Although those methods are also passed a Binder object, their arguments and return types use DynamicMetaObject objects.

The essential piece of information contained by a DynamicMetaObject instance is an expression tree that represents the code that has to be executed to compute its value. It's the DLR's role to stitch together such expression trees to make up efficient call sites that can get compiled into IL code at runtime. This is the place where the object is in total