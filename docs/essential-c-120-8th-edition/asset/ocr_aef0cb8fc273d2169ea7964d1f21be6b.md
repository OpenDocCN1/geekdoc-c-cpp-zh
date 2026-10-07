because, in general, it is necessary to use the XML output in combination with the generated assembly to produce any meaningful documentation. Fortunately, tools such as the free GhostDoc⁶ and the open source project NDoc⁷ can generate documentation.

# Guidelines

> DO XML comments on public APIs when they provide more context than the API signature alone. This includes member descriptions, parameter descriptions, and examples of calling the API.

# Garbage Collection and Weak References

Garbage collection is obviously a core function of the runtime. Its purpose is to restore memory consumed by objects that are no longer referenced. The emphasis in this statement is on memory and references: The garbage collector is responsible only for restoring memory; it does not handle other resources such as database connections, handles (files, windows, etc.), network ports, and hardware devices such as serial ports. Also, the garbage collector determines what to clean up, based on whether any references remain. Implicitly, this means that the garbage collector works with reference objects and restores memory on the heap only. Additionally, it means that maintaining a reference to an object will delay the garbage collector from reusing the memory consumed by the object.

+   6. See https://submain.com/ to learn more about GhostDoc.
7. See https://ndoc.sourceforge.net/ to learn more about NDoc.