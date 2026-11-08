
## std::vector and Other Containers

The collection you are likely to use most is `std::vector`. It is a fast, general-purpose collection similar to `List<T>` in .NET. It is found in the `<vector>` header file.

To add an item to the end of a vector, use the member function `push_back`. To remove an item from the end of a vector, use `pop_back`. You can access items at their index using `[]` the same way you would an array. To add an element or range of elements at a specific zero-based index, use the `insert` member function. To remove an element or range of elements at a specific zero-based index, use the `erase` member function.

A neat feature added in C++11 is the in-place construction functionality provided by the `emplace` and `emplace_back` member functions. Rather than constructing an object and then using `insert` or `push_back` to add it to the vector, you can call `emplace_back` and simply pass it the same arguments you would pass to the constructor for the type that the vector will hold. The vector will then construct and add a new instance of the object without the extra calculations that come with a copy or a move, and without using extra local memory.

The `emplace` function works the same, except you start by passing it an iterator that specifies the location. You can use `c.begin()` or `c.end()` to add items to the beginning or end of the vector. If you have a specific zero-based index you want to emplace an item at, you can use `c.begin() + idx`. You can also subtract from `c.end()` if you want to place an item some number of spaces from the end.

`vector` offers more functionality, so you should definitely explore it further. The `at` member function will give you an item at an index, for example. There are ways to tell the vector to resize its internal capacity so you have more room free—if you knew you would need exactly 125 items, for instance—or so you minimize memory usage—if you added all the elements it will ever need and memory constraints are tight.

In addition to `std::vector`, several similar containers have different use cases. `std::vector` itself is the best choice when you need extremely fast, random access—when you will mostly be adding items to and removing items from the very end of the collection. If you also need to add items frequently to the front of the collection, you should consider using `std::deque` instead.

Use `std::queue` for a first-in, first-out container. Use `std::stack` for a last-in, first-out container.

The `std::map` class provides a sorted dictionary. `std::unordered_map` provides a hash table.

The `std::set` class is a sorted, keyed collection where the item stored is its own key, so each element must be unique. `std::unordered_set` is the unsorted equivalent of `std::set`.

The `std::list` class provides a doubly linked list. `std::forward_list` provides a singly linked list.

## The `<algorithm>` Header

The `<algorithm>` header contains many very useful functions: things such as find, sort, copy, and all their related methods. The best way to learn them is to experiment with them.

## The C Run-Time Library (CRT)

Some functionality from the C Runtime Library can be useful. Generally, the best way to access the library is to include the relevant `<c...>` header file, such as `<cstdlib>`.

## Chapter 14 Visual Studio and C++

### IntelliSense

If you’re using almost any of the Visual Studio keyboard mappings, typing Ctrl+J will bring up IntelliSense. In Visual Studio 2012, IntelliSense should appear automatically in C++. In Visual Studio 2010 and earlier, you need to invoke it manually.

### Code Snippets

Code snippets are a new feature for C++ in Visual Studio 2012. They did not exist in earlier versions. If you’ve never used them in any language, then in a C# project, start typing “for” to begin a for loop; once IntelliSense has chosen the for snippet, press the Tab key twice and watch as a for loop appears complete with automatic fields you can edit. Use the Tab key to switch between fields. When you’re done editing the fields, press Enter. The cursor will be transported within the loop body with the field edits you made appearing as normal text.

Code snippets are particularly nice for switch statements that switch on an enum, since they will automatically populate the switch statement with all of the enum’s members.

### Including Libraries

In C++, it's usually not enough to just include a header file. Normally you need to tell the linker to link against a library that implements the code declared in the header file. To do this, you need to edit the project’s properties, accessible in the **Project** menu as **ProjectName Properties...**

In the properties, under **Configuration Properties > Linker > Input**, one of the fields is **Additional Dependencies**. This is a semicolon-separated list of the **.LIB** files you need to link against. It should end with `%(AdditionalDependencies)` so that any additional libraries linked via MSBuild will be added.

For a typical DirectX 11 Metro-style game, for example, you might see the following:

```
d2d1.lib; d3d11.lib; dxgi.lib; ole32.lib; windowscodecs.lib; dwrite.lib;
xaudio2.lib; xinput.lib; mfcore.lib; mfplat.lib; mfreadwrite.lib; mfuuid.lib;
%(AdditionalDependencies)
```

If you receive a linker error telling you it cannot find a definition of something you are using, find the function or class on MSDN; the documentation will tell you both the header file and the library file you need.

### Generating Assembly Code Files

If you want to view a very close approximation of the assembly code that your code is compiled into, in your project’s properties, under **Configuration Properties > C/C++ > Output Files**, set the **Assembler Output** option to something other than **No Listing**.

I’d recommend either **Assembly-Only Listing (/FA)** or **Assembly with Source Code (/FAs)**. **Assembly-Only Listing** sprinkles enough line-number comments that you can usually cross-reference with your source code files to see what C++ code corresponds with the assembly code. That can be helpful if you want one place to see everything rather than flipping back and forth between whatever you’ve opened the .ASM file in (I use Notepad++) and Visual Studio.

Note that the generated assembly uses MASM macros (find them on MSDN). If you don’t know what a particular assembly instruction means (e.g., LEA), you can search the internet for it or download the appropriate programming manual from Intel’s site (assuming x86/Itanium), AMD’s site (assuming x64) or ARM Holdings’ site (assuming ARM). If you’ve never learned any assembly, I definitely recommend doing so (try creating a simple Windows console app).

Understanding assembly gives you a better understanding of how computers really work internally. Combine that with the knowledge that computers are all hardwired to begin executing the same code every time they are powered on (traditionally the BIOS on PCs, though that is now being replaced by UEFI), and the mystery of how and why computers work quickly begins to fade.

### Terrifying Build Errors

If you come across a build error that looks completely horrible, chances are it’s from the linker. You’ll see messages like this, for instance:

```
Error    2    error LNK2019: unresolved external symbol "__thiscall
SomeClass::SomeClass(wchar_t const *)" (??0SomeClass@@QAE@P?W@Z) referenced in
function "void __cdecl DoSomething(void)" (?DoSomething@@YAXXZ)
D:\VS2010\ProjCppSandbox\CppSandbox\CppSandbox.obj    CppSandbox
```

All that’s saying is it cannot find a function you said it should be able to find. In this case, I added the `inline` keyword to a constructor function definition in the CPP file without remembering to relocate that definition to the header file. Any inline functions need to be in the header so the linker won’t have to look for it.

All those ??s and @@s are just how C++ mangles names when it has compiled code into object files. Name mangling is internally consistent for the compiler in question, but the ISO/IEC standard doesn’t mandate any particular schema for name mangling. Different compilers can, and often will, mangle things differently.

Normally, if you see a horrifying build error message, chances are it’s from the linker, and it’s an unresolved symbol error. If it’s saying it can’t find something you wrote, then check to make sure your declaration in the header file matches the definition, usually in the code file but maybe in the header, or maybe you forgot to write it, or maybe you declared it inline but still have it in the code file.

An example of this is in the previous case: my `SomeClass::SomeClass(wchar_t const *)` constructor function (I always write `const type` not `type const`, so even that bit is reconstructed).

If it’s someone else’s function or other symbol, then chances are you didn’t tell the linker about the .LIB file that contains it.

In .NET, you just add a reference to an assembly to get both the declaration bits and the actual definition all in one. In C++, the declaration is the header file, while the definition code—excluding inline code, which needs to be in the header file too—is in a separate library. Search the MSDN library for the missing symbol and find the name of the library file you need to add.

C++ build errors can look pretty scary, especially when you receive a build error involving a template. Those can make you want to quit. But don’t. Never let the horrible error messages win. First, figure out if it’s coming from the compiler (it’ll have a `C####` error number format) or the linker (`LNK####` error number format).

If from the compiler, it usually means a syntax error. Check things like whether you forgot the `#pragma once` at the top of your header file. Another problem could be where you used something from the Standard Library (e.g., `endl`) but forgot to have a `using namespace std;` or to prefix it with `std::` (i.e., `std::endl`).

You can do either or both, but you must do at least one. Some things might be in a different namespace. In Visual Studio 2010, some functionality is in the `stdext` namespace, for example. The same goes for any namespaces in your own code.
