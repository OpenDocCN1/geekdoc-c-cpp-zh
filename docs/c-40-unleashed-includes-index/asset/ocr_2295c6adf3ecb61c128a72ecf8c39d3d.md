However, I used the wrong letter case on the name of the field in the setter: Instead of writing name, I wrote Name, which is the name of the property itself. That's the source of the unbounded recursion. Assigning to a property calls its setter, and we're doing this from the setter itself. The reason I didn't run into this problem outside the deserializer's case was because my types had constructors defined for use elsewhere, which directly assigned to the underlying fields:

```
public Student(string name)
{
    this.name = name;
}
```

Three lessons learned here are as follows:

+   - Be sure to have high code coverage with unit tests, even for things that seem as trivial as property setters.
+   - Naming conventions can help reduce the likelihood of introducing problems. Ever since, I prefix my fields with an underscore.
+   - Don't blame others blindly, especially when talking about framework code that's highly tested. That blame will bounce back at you quickly.

So the next time you see a stack overflow and you haven't intentionally written a deeply recursive algorithm, you can be quite sure you have some bug somewhere in your code.

Notice that the runtime doesn't enable you to catch disastrous exception types. No matter how hard you try, the runtime will give up all hope and terminate the process to avoid risking instabilities, data corruption, and so on.

# TIDBIT FOR HARDCORE DEBUGGERS

Sometimes when people get deep into debugging managed code application crashes using advanced debuggers like WinDbg with SOS (more on that later), they get misled by the presence of an OutOfMemoryException object that you can find on the heap. Figure 8.4 uses SOS to prove the existence of this instance on the managed heap. For some reason, this sometimes leads novices to conclude an out-of-memory condition caused the program to fail. Chip vendors have probably benefited from this as developers recommended buying more RAM, but this is a completely wrong conclusion for reasons we're explaining here.

OutOfMemoryException doesn't necessarily (and usually doesn't) mean there's not enough physical memory in the machine. All it means is there's insufficient address space left in the executing process for the garbage collector to allocate additional space for the managed object heap. An in-depth discussion about virtual memory and address space is beyond the scope of this book, but you'll find such information in every self-respecting book on operating systems.