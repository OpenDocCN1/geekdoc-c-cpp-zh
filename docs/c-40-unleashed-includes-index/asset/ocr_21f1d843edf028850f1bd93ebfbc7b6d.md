Notice how simple the code on the right (which is the developer's playground to add custom logic to the form) looks, in contrast to what it would have looked like before C# 2.0. In practice, you almost never have to inspect the generated code that appears on the left and is stored in a .Designer.cs file.

The key essence of this feature lies in the fact that a class's (or struct's or interface's) members can be spread across multiple files. To use it, you just prefix the class, struct, or interface keyword with *partial*. One or more partial definitions of the type can now occur throughout all the files that get compiled. During compilation, it's the compiler's job to paste together all the fragments that make up the same type.

> > **PARTIAL METHODS**
> >
> > C# 3.0 introduced another "partial definition" feature, called partial methods. We take a look at them in Chapter 10. The common theme between all those features is to aid in code-generation scenarios where a code generator takes responsibility for one part of a type definition and the developer takes care of the other parts.

# ## Summary

Types are the containers for state and operations. Although we haven't talked about object-oriented programming yet, we've learned about various essential features of types. First, we contrasted classes and structs, discussing concepts of references and values. Related to this, we learned about memory management provided by the runtime, in particular the stack and the heap. Finally, the concept of boxing was explained.

In preparation for the next few chapters, we also talked about common aspects of a type's members. This includes the notion of visibility and the difference between static- and instance-level members. To wrap up our discussion of members, we also learned how to use partial types to split the definition of a type's members across different code files.

Now that we've learned about types as containers of members, we're ready to look into them in more detail. The next chapters discuss the code aspect of types being methods, followed by an exploration of the data aspect exposed through fields, properties, and indexers. Constructors and finalizers are covered as well.