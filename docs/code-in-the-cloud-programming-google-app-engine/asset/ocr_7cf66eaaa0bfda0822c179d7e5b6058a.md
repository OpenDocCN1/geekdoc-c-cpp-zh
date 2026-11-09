any differently than any other attribute. But that’s going to be really awkward. So what can we do?

Answering that question isn’t trivial, and it brings us to one of the most important factors in designing a good datastore model: where do you put the dividing line between different objects? And how do you describe relationships between objects? In datastore, you do that with references.

# Datastore Keys and References

When it comes to handling the value of the children attribute in the datastore, we’ve got two real choices: we can either find a way of encoding the structure of a directory as a string and then put that string into an attribute, or we can treat the children attribute as a special case. We’ll look at some details of the trade-offs between those two later; but for now, we’ll just go the easy route and treat children as a special case. Directory structure is a key detail in a filesystem, so while it may seem a bit hacky, it really is important enough to justify treating it specially.

But either way, we’re coming up against another important factor. A file in a directory is an independent object. If you think in terms of a classical object model, a file isn’t a *part-of* the directory that contains it; it’s a standalone object which is *referenced-by* its parent directory. This distinction is particularly important in a system like datastore.

Suppose we made files a part of the directory that encloses them. Then whenever we retrieved the root directory of the filesystem from the datastore, we would need to load the entire filesystem out of the datastore. The root directory ultimately contains every file and directory in the system; if it just contained parts of them, they’ll be stored and retrieved with it. In addition, we won’t even be able to retrieve an individual file: it will only exist as an attribute within the root directory.

That’s definitely not what we want.

We want our filesystem to be a collection of independent objects. In terms of a classical in-memory object model, what we want is a pointer: we don’t want the directory to contain its children; we want it to point to its children.

In datastore, the equivalent of a pointer in a language like C++ is called a *reference*. A reference isn’t like a C++ reference, which is really just another name for a pointer. An object-store reference is an identifier that uniquely identifies some other object in the datastore. It’s almost