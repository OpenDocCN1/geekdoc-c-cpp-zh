The variety and purpose of the various libraries available to a C compiler depend on what you plan to do. C language library packages can be found for free and downloaded from the Internet. For example, a hardware manufacturer may provide a library you can use to program its specific device.

![](bbox=[0.15, 0.3, 0.22, 0.42])

+   - Libraries are linked in only when creating a Code::Blocks project. You cannot link in a library for an individual source code file.
+   - Traditionally, C libraries are stored in the /usr/lib folder, though downloaded libraries might be found in /usr/local/lib or elsewhere. Command-line compilers automatically look in these locations.
+   - The -L switch for a command-line compiler can be specified to direct the compiler to look in a specific folder for a library. For example:

```
clang -L/usr/local/share/lib -lcompress main.c
```

The preceding command directs the clang compiler to look in the /usr/local/share/lib folder for the compress library.