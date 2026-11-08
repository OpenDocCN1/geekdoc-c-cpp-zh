# # Chapter 14 Visual Studio and C++

# ## IntelliSense

If you’re using almost any of the Visual Studio keyboard mappings, typing Ctrl+J will bring up IntelliSense. In Visual Studio 2012, IntelliSense should appear automatically in C++. In Visual Studio 2010 and earlier, you need to invoke it manually.

# ## Code Snippets

Code snippets are a new feature for C++ in Visual Studio 2012. They did not exist in earlier versions. If you’ve never used them in any language, then in a C# project, start typing “for” to begin a for loop; once IntelliSense has chosen the for snippet, press the Tab key twice and watch as a for loop appears complete with automatic fields you can edit. Use the Tab key to switch between fields. When you’re done editing the fields, press Enter. The cursor will be transported within the loop body with the field edits you made appearing as normal text.

Code snippets are particularly nice for switch statements that switch on an enum, since they will automatically populate the switch statement with all of the enum’s members.

# ## Including Libraries

In C++, it's usually not enough to just include a header file. Normally you need to tell the linker to link against a library that implements the code declared in the header file. To do this, you need to edit the project’s properties, accessible in the **Project** menu as **ProjectName Properties...**

In the properties, under **Configuration Properties > Linker > Input**, one of the fields is **Additional Dependencies**. This is a semicolon-separated list of the **.LIB** files you need to link against. It should end with `%(AdditionalDependencies)` so that any additional libraries linked via MS Build will be added.

For a typical DirectX 11 Metro-style game, for example, you might see the following:

```
d2d1.lib; d3d11.lib; dxgi.lib; ole32.lib; windowscodecs.lib; dwrite.lib;
xaudio2.lib; xinput.lib; mfcore.lib; mfplat.lib; mfreadwrite.lib; mfuuid.lib;
%(AdditionalDependencies)
```

If you receive a linker error telling you it cannot find a definition of something you are using, find the function or class on MSDN; the documentation will tell you both the header file and the library file you need.

# ## Generating Assembly Code Files

If you want to view a very close approximation of the assembly code that your code is compiled into, in your project’s properties, under **Configuration Properties > C/C++ > Output Files**, set the **Assembler Output** option to something other than **No Listing**.

I’d recommend either **Assembly-Only Listing (/FA)** or **Assembly with Source Code (/FAs)**. **Assembly-Only Listing** sprinkles enough line-number comments that you can usually cross-reference with your source code files to see what C++ code corresponds with the assembly code. That can be helpful if you want one place to see everything rather than flipping back and forth between whatever you’ve opened the .ASM file in (I use Notepad++) and Visual Studio.