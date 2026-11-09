for all of these objects, and in many situations, this is impossible because you won't have access to the private fields of the other objects!

This example shows how to create an object that constantly resurrects itself and never dies—but you don't usually want objects to do this. It's far more common to conditionally set a root to reference the object inside the **Finalize** method.

> **Note** Make sure that you call **ReRegisterForFinalize** no more than once per resurrection, or the object will have its **Finalize** method called multiple times. The reason is that each call to **ReRegisterForFinalize** appends a new entry to the end of the finalization list. When an object is determined to be garbage, all of these entries move from the finalization list to the freachable queue, making the object's **Finalize** method called multiple times.

At the end of this chapter's "Generations" section, I present a **GCNotification** class that uses resurrection in a useful and meaningful way.

# ## Generations

As I mentioned near the beginning of the chapter, generations are a mechanism within the CLR garbage collector whose sole reason for being is to improve an application's performance. *A generational garbage collector* (also known as an *ephemeral garbage collector*, although I don't use the latter term in this book) makes the following assumptions:

+   - The newer an object is, the shorter its lifetime will be.
+   - The older an object is, the longer its lifetime will be.
+   - Collecting a portion of the heap is faster than collecting the whole heap.

Numerous studies have demonstrated the validity of these assumptions for a very large set of existing applications, and these assumptions have influenced how the garbage collector is implemented. In this section, I'll describe how generations work.

When initialized, the managed heap contains no objects. Objects added to the heap are said to be in generation 0. Stated simply, objects in generation 0 are newly constructed objects that the garbage collector has never examined. Figure 21-8 shows a newly started application with five objects allocated (A through E). After a while, objects C and E become unreachable.

![](bbox=[0.15, 0.945, 0.53, 0.98])

**FIGURE 21-8** A newly initialized heap containing some objects, all in generation 0. No collections have occurred yet.