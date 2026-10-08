
Pirkle, Will. 2012. Designing Audio Effects Plug-Ins in C++, Chap. 8. Burlington: Focal Press.

Steiglitz, Ken. 1996. A DSP Primer with Applications to Digital Audio and Computer Music. Menlo Park: Addison Wesley.

## Chapter 2
## Writing Plug-ins

The plug-in core is the code you need to implement that deals with the details of communicating with the client, setting up a rendering system and handling a Graphical User Interface (GUI or UI). While the implementation details are very different, the fundamental theory of operation is the same for all three (and practically any other plug-in format there). When you learn to fly, you find that the fundamentals of pitch, drag, yaw and roll are all for the tiniest trainer to fighter; the interfaces you deal with are very different. In this chapter, we start with the similarities and introduce the RackAFX-plug-in API and philosophy. We will explore the VST3 and AU platforms in depth. If you have never written a plug-in, we strongly suggest starting with RackAFX—in fact we still start every project in RackAFX and then port them out to VST3 and AU debugging the core.

## 2.1 Dynamic-Link Libraries

C++ compilers include sets of pre-compiled libraries of functions for you to use in your projects. The most common of these is the math library. If you try to use the sin() method, you will typically get an error when you compile that "sin() is not defined." In order to use this function, you need to link to the library that contains it. The way you do this is by placing #include at the top of your file. When you do this, you are statically linking to the math.h library, a pre-compiled set of functions in a special file called a Library (.lib) in Windows or a Framework in MacOS. Static linking replaces the function call with the precompiled code from the library. In this way, the extra code is compiled into your executable. You cannot compile the functions.

To build a component that extends the application's functionality after the application has been compiled and sold to the customer requires a different strategy. The solution is to link to functions at runtime. This means that precompiled functions exist in a separate file that the client will know about and communicate with only after it starts. This kind of linking is called dynamic linking or explicit linking. The file that contains the new functions is called Dynamic-Link Library or DLL. In Windows, the file typically uses the extension .dll; however, in VST3, you rename the extension .v3. In AU, the DLL extension is.

In order to use the code in a DLL, a client must perform two activities:

- 1. load the DLL into the process address space
- 2. establish the communication mechanism for functions to be called from the C++

We won't worry about these client-side details, but it is important to understand how C++ and base classes play a role in plug-in development.

## 2.2 C and C++ Style DLL

A DLL written in the C programming language consists of a set of stand-alone functions. There is no main() function that can be defined and implemented in one file or be broken into an interface; the DLL performs a set of isolated functions. A problem with using the C programming language to write a DLL is that in C (and C++) the brackets ('{}') define the scope of the function. Any variable declared inside a function, after the first open bracket ('{'), is only defined for the duration of the function. After the closing curly bracket ('{}') is encountered, the variable ceases to exist.

A fundamental problem is that the data declared in a function cannot persist from one call to the next. One solution involves using global variables, which is generally frowned upon. Another is for the DLL to dynamically declare a data structure that will hold all persistent variables and then pass a pointer to this data back to the client. This is very similar to the way callback functions work. During subsequent calls to the DLL, the client passes the pointer back to the DLL so that it may operate on the persistent data. When the DLL is no longer needed, it clears the memory by deleting the structure.

In the C++ programming language, the class-type defines an object that is a collection of member variables and member functions that can operate on those variables. By packing a plugin-in as a C++ class, you get several advantages: first, all of the C++ (inheritance, encapsulation, polymorphism, etc.) are available during the coding process. Second, rather than allocating a data structure and returning a pointer to the DLL, the client can create a new instance of the plugin-object and pass a pointer to the client. The function that is called is the creation. With a plug-pointer, the client can simply call functions on the object—it does not have to communicate with the DLL until it is time to unload the DLL, or create another instance of the plugin-object. This leads to a third advantage over the C-based DLL: the client can create multiple instances easily. The DLL can serve multiple instances of the object. Sometimes, the plugin-in is referred to as a server and this becomes another kind of client-server.

## 2.3 The Application Programming Interface (API)

In order for the client-server scheme to work, both the client and DLL/plugin-in must agree on the naming of the functions. This includes the creation function and all of the functions that will be called on the plugin-in. The plugin-object must implement other functions that the client doesn't know about, but they must agree on a basic set of them. Rules must be set up to define the sequence of function calls; the plugin-in's author (that's you) will need to understand how the client uses the object. The client must make sure that it establishes these rules, adheres to them in future versions to avoid breaking the plugin-in. On the other hand, the plugin-in may promise to implement the basic required functions properly to make the plugin-in work and not crash the client. So, you can see that there is an implicit contract between the client and DLL server. This contract is the Application Programming Interface or API. It is a definition of the functions an object must implement to be considered a proper plugin-in, as well as any additional functions that may be called or overridden. It defines the function prototypes and describes how the functions will be called and used. The client manages the API and makes it available for programmers to create plugin-ins for target client.

C++ is especially useful. Since the plugin-in is an instance of a C++ object, the client can specify that the plugin-in is derived of a special base class that the manager defines. The base class is to be abstract, containing virtual functions that the client declares. These virtual functions provide the common functionality of the plugin-in. There are two options here:

- the manager defines the base class as abstract as there provides default implementations of the functions. Typically, the implementations do nothing but-
- the manager defines the base class as abstract as there provides default implementations of the functions. Typically, the implementations do nothing but-

## 2.4 API Comparisons

Although the various plugin-in APIs differ in their implementation, VST3 certainly wins the prize for most number of supporting files. In VST3, the process() function becomes so large that we split it into three functions. In RackAFX there is no GUI to write since you will have to write your own in AU (and it's in the Objective-C programming language). You can see that each platform is different in complexity.
