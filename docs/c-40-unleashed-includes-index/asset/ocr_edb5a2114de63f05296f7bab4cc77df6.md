In our case, the assembly has been stored on disk as a file, more specifically as a file called hello.exe. In .NET Reflector, we can observe this by the child node to our assembly, which is the hello.exe module. Assemblies can consist of one or more modules, but the most common case is to have just one module. We won't go into detail on this topic for now.

Next, we encounter a node with a {} logo. This indicates a namespace and is a result of .NET Reflector's decompilation intelligence, as the CLR does not know about namespaces by itself. Namespaces are a way to organize the structure of APIs by grouping types in a hierarchical tree of namespaces (for example, System.Windows.Forms). To the CLR, types are always referred to—for example, in IL code—by their fully qualified name (like System.Windows.Forms.Label). In our little hello.exe program we didn't bother to declare the Program class in a separate namespace, so .NET Reflector shows a "-" to indicate the global namespace.

Finally, we arrive at our Program type with the Main method inside it. Let's take a look at the Main method now. Select the tree node for Main and press the spacebar key. Figure 3.13 shows the result.

![](bbox=[0.1, 0.64, 0.62, 0.88])

FIGURE 3.13 Disassembling the Main method.

The pane on the right shows the decompiled code back in C#. It's important to realize this didn't use the hello.cs source code file at all. The hello.exe assembly doesn't have any link back to the source files from which it was compiled. "All" .NET Reflector does is reconstruct the C# code from the IL code inside the assembly. You can clearly see that's the case because the Main method does only contain two statements according to .NET Reflector, even though we wrote it with three statements instead. .NET Reflector's view on our assembly is semantically correct, though; we could have written the code like this.

Notice the drop-down box in the toolbar at the top. Over there we can switch to other views on the disassembled code (for example, plain IL). Let's take a look at that, too, as shown in Figure 3.14.