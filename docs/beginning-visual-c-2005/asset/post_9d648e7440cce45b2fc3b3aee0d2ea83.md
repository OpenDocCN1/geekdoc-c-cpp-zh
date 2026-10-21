
## Writing Your Own DLLs

Chapter 9 discussed how a C++/CLI class library is stored in a .dll file. Dynamic link libraries are also used extensively with native C++ applications. A complete discussion of DLLs in native C++ applications is outside the scope of a beginner’s book, but they are important enough to justify including an introductory chapter on them. In this chapter, you will learn about:

- DLLs and how they work
- When you should consider implementing a DLL
- What varieties of DLL are possible and what they are used for
- How you can extend MFC using a DLL
- How to define what is accessible in a DLL
- How to access the contents of a DLL in your programs

## Understanding DLLs

Almost all programming languages support libraries of standard code modules for commonly used functions. In native C++ you’ve been using lots of functions that are stored in standard libraries, such as the ceil() function that you used in the previous chapter, which is declared in the <cmath> header. The code for this function is stored in a library file with the extension .lib, and when the executable module for the Sketcher program was created, the linker retrieved the code for this standard function from the library file and integrated a copy of it into the .exe file for the Sketcher program. If you write another program and use the same function, it will also have its own copy of the ceil() function. The ceil() function is statically linked to each application and is an integral part of each executable module, as illustrated in Figure 18-1.

![](img/2359b0c604600c58fba3539c738a356e_943_0.png)

Although this is a very convenient way of using a standard function with minimal effort on your part, it does have its disadvantages as a way for several concurrently executing programs to make use of the same function in the Windows environment. A statically linked standard function being used by more than one program concurrently is duplicated in memory for each program using it. This may not seem to matter much for the ceil() function, but some functions — input and output, for instance — are invariably common to most programs and are likely to occupy sizable chunks of memory. Having these statically linked would be extremely inefficient.

Another consideration is that a standard function from a static library may be linked into hundreds of programs in your system, so identical copies of the code for them will be occupying disk space in the .exe file for each program. For these reasons, an additional library facility is supported by Windows for standard

functions. It’s called a dynamic link library, and it’s usually abbreviated to DLL. This allows one copy of a function to be shared among several concurrently executing programs and avoids the need to incorporate a copy of the code for a library function into the executable module for a program that uses it.

## How DLLs Work

A dynamic link library is a file containing a collection of modules that can be used by any number of different programs. The file usually has the extension .dll, but this isn’t obligatory. When naming a DLL, you can assign any extension that you like, but this can affect how they’re handled by Windows. Windows automatically loads dynamic link libraries that have the extension .dll. If they have some other extension, you will need to load them explicitly by adding code to do this to your program. Windows itself uses the extension .exe for some of its DLLs. You have likely seen the extensions .vbx and .ocx, which are applied to DLLs containing specific kinds of controls.

You might imagine that you have a choice about whether or not you use dynamic link libraries in your program, but you don’t. The Win32 API is used by every Windows program, and the API is implemented in a set of DLLs. DLLs are fundamental to Windows programming.

Connecting a function in a DLL to a program is achieved differently from the process used with a statically linked library, where the code is incorporated once and for all when the program is linked to generate the executable module. A function in a DLL is connected only to a program that uses it when the application is run, and this is done on each occasion the program is executed, as Figure 18-2 illustrates.

Figure 18-2 shows the sequence of events when three programs that use a function in a DLL are started successively and then all execute concurrently. No code from the DLL is included in the executable module of any of the programs. When one of the programs is executed, the program is loaded into memory, and if the DLL it uses isn’t already present, it too is loaded separately. The appropriate links between the program and the DLL are then established. If, when a program is loaded, the DLL is already there, all that needs to be done is to link the program to the required function in the DLL.

Note particularly that when your program calls a function in a DLL, Windows will automatically load the DLL into memory. Any program subsequently loaded into memory that uses the same DLL can use any of the capabilities provided by the same copy of the DLL because Windows recognizes that the library is already in memory and just establishes the links between it and the program. Windows keeps track of how many programs are using each DLL that is resident in memory so that the library remains in memory as long as at least one program is still using it. When a DLL is no longer used by any executing program, Windows automatically deletes it from memory.

MFC is provided in the form of a number of DLLs that your program can link to dynamically, as well as a library that your program can link to statically. By default, the Application wizard generates programs that link dynamically to the DLL form of MFC.

Having a function stored in a DLL introduces the possibility of changing the function without affecting the programs that use it. As long as the interface to the function in the DLL remains the same, the programs can use a new version of the function quite happily, without the need for recompiling or re-linking them. Unfortunately, this also has a downside: it’s easy to end up using the wrong version of a DLL with a program. This can be a particular problem with applications that install DLLs in the Windows System folder. Some commercial applications arbitrarily write the DLLs associated with the program to this folder without regard to the possibility of a DLL with the same name being overwritten. This can interfere with other applications that you have already installed and, in the worst case, can render them inoperable.

## Run-Time Dynamic Linking

The DLL that you’ll create in this chapter is automatically loaded into memory when the program that uses it is loaded into memory for execution. This is referred to as **load-time dynamic linking**, or **early binding**, because the links to the functions used are established as soon as the program and DLL have been loaded into memory. This kind of operation was illustrated in Figure 18-2; however, this isn’t the only choice available. It’s also possible to cause a DLL to be loaded after execution of a program has started. This is called **run-time dynamic linking** or **late binding**. The sequence of operations that occurs with this is illustrated in Figure 18-3.

![](img/2359b0c604600c58fba3539c738a356e_945_0.png)

Figure 18-2

![](img/2359b0c604600c58fba3539c738a356e_946_0.png)

Figure 18-3

Run-time dynamic linking enables a program to defer linking of a DLL until it’s certain that the functions in a DLL are required. This allows you to write a program that can choose to load one or more of a number of DLLs based upon input to the program so that only those functions that are necessary are actually loaded into memory. In some circumstances, this can drastically reduce the amount of memory required to run a program.

A program implemented to use run-time dynamic linking calls the Windows API function LoadLibrary() to load the DLL when it’s required. The address of a function within the DLL can then be obtained using a function GetProcAddress(). When the program no longer has a need to use the
