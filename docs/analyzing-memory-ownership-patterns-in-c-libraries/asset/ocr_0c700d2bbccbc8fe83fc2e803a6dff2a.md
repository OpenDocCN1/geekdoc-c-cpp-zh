# Table 2. Number of inferred reference counting annotations. “Ref/Unref” refers to the number of inferred IncRef and DecRef function pairs, rather than single functions.

| Library Analyzed | Reference Counting | | | |
|---|---|---|---|---|
| Name | Functions | Allocators | Finalizers | Ref/Unref |
| cairo | 379 | 2 | 2 | 4 |
| dbus-1 | 804 | 36 | 8 | 11 |
| exif | 142 | 16 | 5 | 7 |
| fontconfig | 196 | 51 | 8 | 3 |
| freetype | 289 | 9 | 6 | 3 |
| gio-2.0 | 1772 | 58 | 11 | 9 |
| glib-2.0 | 1529 | 228 | 39 | 16 |
| gobject-2.0 | 394 | 15 | 3 | 1 |
| soup-2.4 | 530 | 46 | 6 | 3 |

```
void exif_mem_free(ExifMem *mem, void *d)
{
    if (!mem) return;
    if (mem->free_func) {
        mem->free_func(d);
        return;
    }
}
```

# Figure 11. Finalizer from exif library

allocators, (3) the number of functions that are finalizers, and (4) the number of IncRef and DecRef function pairs. As with our ownership transfer analysis, the reference counting analysis requires an accurate view of the allocators and finalizers present in each library. The dbus-1 library required two manual annotations, exif required four, gobject required one, and glib required seven in order for all of the allocators and finalizers to be recognized. Some of these libraries use custom memory allocators, while others have finalizers that do not quite match the notion of a finalizer that our tools use because they include extra not-NULL checks. Figure 11 shows an example. On line 4, this finalizer checks that a function pointer that it calls is not-NULL. Extending the allocator and finalizer identification analyses is beyond the scope of this work.

This analysis is useful in several ways. First, it alerts users that their library uses reference counting. Our experiments revealed reference-counted types in libraries where we did not expect them, including ical and libusb. Reference counting is not the primary resource management discipline in either library, but is still important yet not apparent from a visual scan. More importantly, even in cases where reference counting is the primary resource management discipline, our reference counting analysis identifies both polymorphic IncRef/DecRef functions and the types they operate on. For example, in dbus-1 we recognize dbus_auth_unref and dbus_auth_ref as polymorphic managers of reference counts for three related types: DBusAuthClient, DBusAuthServer, and DBusAuth.

The gio-2.0 library highlights the importance of the reference counting analysis in the presence of polymorphic reference counters. While gio-2.0 has 9 IncRef/DecRef pairs that are identified by the analysis, it defines a further 138 types that are managed by the g_object_unref and g_object_ref functions defined in the gobject-2.0 library. Note that the 9 types with their own reference counting functions cannot be managed with the generic gobject-2.0 reference counting functions, though nothing in the names of the types reveals this. Section 7.2 describes two algorithms for recognizing which types are managed by polymorphic reference counting functions. The first relies on the presence of type-specific finalizers and the second relies only on structural subtyping. The second algorithm

has been more reliable in practice, identifying 23 types as managed by the gobject-2.0 reference counting functions that were missed by the first algorithm. The first algorithm misses these types because they have no type-specific resources that need to be finalized, and so do not define a finalizer. However, they are still structural subtypes of GObject, so the second algorithm recognizes them.

# 9. Related Work

The C/C++ leak detector of Heine and Lam [6] is very similar in spirit to our work. They present an inference algorithm based on inequality constraints to assign an owner to each object in a program. Our algorithms work on partial programs (libraries) and are formulated in terms of symbolic access paths. Our major contributions beyond their work are to (1) recognize ownership semantics for C objects with a generalized notion of allocators and finalizers (instead of C++) and (2) incorporate shared ownership via reference counting and inferred contracts on function pointers used in library code. Rayside and Mendel [17] take a more dynamic approach with ownership profiling; they report detailed hierarchical ownership information that is more precise than what we can achieve statically. Negara et al. [13] describe an inference algorithm based on liveness analysis for identifying ownership transfer semantics in message passing applications. In cases where ownership can be proved to transfer to another process via message passing, the copy of the message can be skipped and the receiving process can assume ownership of the message directly. Boyapati et al. [1] address ownership at the type level with work on ownership types. Müller and Rudich [12] extend Universe Types to support ownership transfer. Their notion of temporary aliases correspond closely to our transient references. In effect, we infer ownership types for C. Focusing specifically on memory, Wegiel and Krintz [20] discuss methods for sharing heap-allocated objects between different managed run-time environments. They do not need to establish an owner for each heap object because the run-time environments are able to cooperate and safely share objects. Since one of our run-time systems is C, which has no facilities for such object sharing, we must infer ownership.

As discussed in section 7, we do not verify the correctness of reference count handling in the libraries we analyze. Emmi et al. [4] present an analysis to perform this complex verification building on the Blast model checker. Our work is complementary in that Emmi et al. require manual specification of the set of reference-counted types, which could be automated with our analysis.

# 10. Conclusion

We have described an ownership model for C resources to make sharing resources between languages in polyglot programs safer. Documenting the ownership properties of even moderately large programs by hand is difficult and labor-intensive. We have described the allocator and finalizer analyses of Ravitch et al. in terms of our ownership model. We have discussed the difficulty in relying only on an escape analysis to model the ownership of objects in C libraries: many manual annotations are required to compensate for the prevalence of escaping function parameters when true ownership transfer is rare. We addressed this difficulty by describing a new ownership transfer analysis based on our ownership model. We also argue that the results of an escape analysis are still useful for understanding the semantics of libraries. We presented a scalable and composable escape analysis to further reduce the number of false positive escape annotations. We have described trade-offs for this escape analysis in context and field sensitivity that are suitable for analyzing an important class of incomplete program: library code. We have also presented an analysis to automatically