
![](img/e073a4882197be4ab61103cbe0bcb394_46_0.png)

## Figure 1.2: Displaying the Compilation and Execution Processes of JIT Compiler

Figure 1.2 demonstrates the process that the IL code goes through before the application code is actually executed.

In contrast to the managed code, unmanaged code directly compiles to the machine code and runs on the machine where it has been compiled. It does not have services, such as security or memory management, which are provided by the runtime.

## Memory Management

One of the most important services that the CLR provides during managed execution is the automatic memory management. The CLR uses garbage collector to manage the allocation and release of memory for an application. This feature of CLR proves beneficial to the developers since it reduces the burden of writing codes to manage memory while developing managed applications. Automatic memory management removes many common problems, such as forgetting to free an object which results in memory leak, or attempting to access memory for an object that is already free.

## CTS

The CTS is an integral part of the runtime and helps to support cross-language communication. It specifies certain guidelines for declaring, using, and managing types at runtime. The functions performed by the CTS are as follows:

- Helps in cross-language communication, type safety, and high-performance execution of code by establishing a framework
- Supports an object-oriented model for implementation of different programming languages
- Specifies guidelines for different languages, ensuring the scope of proper interaction between their objects
- Supports primitive data types, such as Boolean, Byte, Char, and Int32, that are used in the process of development of an application

The CTS can be classified into two data types, value type and reference type. The value type variables are managed by CLR and can store their values in either the stack or heap memory. The garbage collector manages the memory allocated to these types by releasing the memory space of variables when they are no longer in use. An instance of a value type, such as string, has its value allocated on the stack, while an instance of a reference type, such as arrays, has only a reference to its actual value allocated on the stack.

Variables declared as value types have their own separate copy of data; and therefore, any operation on one variable does not affect the other variables. On the other hand, variables that are declared as reference types always share the same copy of data or point to a same object; therefore, any operation performed in one variable directly affects another variable that refer the same instance.

Figure 1.3 shows the hierarchy of the data types:

![](img/e073a4882197be4ab61103cbe0bcb394_47_0.png)

Figure 1.3: Displaying Hierarchical Representation of Different Data Types

## Metadata and Assemblies

A metadata is the self description of a program in the binary format. In other words, metadata contains the information of the classes, methods, and other elements used in a program. This information is stored in a CLR Portable Executable (PE) file or in the memory. When you compile the code in a PE file, the metadata is inserted into one part of the file, while the code is converted into IL and inserted into the other part of the file. The metadata describes every data type and member of your program. When the code is in the run mode, the CLR loads the metadata into the memory and finds information about the classes and members. The metadata of a program includes:

- Assembly information, such as its identity which can be name, version, culture, public key, the types of assemblies, other referenced assemblies, and security permissions
- Information about types, such as name, visibility, base class, interfaces used, and members (methods, fields, properties, events, and nested types)
- Attribute information that modifies the types and members of a class

After providing the listed information, CLR is able to create objects, access data, and call member functions. Assemblies are packaged into units containing programs and libraries. An assembly contains a self-describing binary file, which can be either Dynamic Link Library (DLL) or Executable (EXE) file. It also contains a collection of types, such as classes, interfaces, and structures. A single assembly can contain multiple code files or a single code file can have more than one assembly.

Assemblies can be of two types, static or dynamic. Static assemblies include interfaces, classes, and resources. These assemblies are stored in the PE files on a disk. Using .NET Framework, you can create dynamic assemblies, which run directly from the memory without being saved to disk before execution. However, after execution, you can save them on the disk.

Let’s explore more about assemblies in the following sections:

- Assembly contents
- Assembly manifest
- Global Assembly Cache (GAC)
- Strong name assemblies
- Private and Shared assemblies
- Side-by-Side execution

## Assembly Contents

Typically, an assembly is a logical unit that consists of four elements – the manifest, type metadata, IL code that implements the types, and a set of resources, such as bitmaps, and Joint Photographic Experts Group (JPEG) files. These elements can be grouped in the form of a single file or a collection of multiple files.

## Assembly Manifest

Every assembly contains data that describes how elements are related to each other within the assembly. Assembly manifest is a file that contains the metadata of the assembly, which is the information of version requirements and security identity of the assembly. The manifest can be stored either in a PE file with IL code or in a standalone PE file that contains only the manifest information.

Table 1.1 lists the information stored in the assembly manifest:

| Information | Description |
|---|---|
| Assembly name | Specifies the name of the assembly. |
| Version number | Indicates a major version number, a minor version number, and a revision and build number. The CLR uses these numbers to enforce the version policy. |
| Culture | Provides information about the culture or language that the assembly supports. |
| Strong name information | Indicates a public key, when the assembly contains a strong name, which is a hash token to encrypt the name and content along with the public key in the assembly. |
| List of all files in the assembly | Contains the hash token and name of each file contained in the assembly. Hash token is an alphanumeric string that is generated as per the contents of a file. Note that all files of an assembly must be stored in the same directory containing the assembly manifest file. |
| Type reference information | Contains the information required to map a type reference with a file that contains the declaration and implementation of this type reference. Types exported from the assembly use the type reference information. |
| Information on referenced assemblies | Contains a list of assemblies that are statically referenced by the assembly. An assembly reference contains the information of the assembly, such as the dependent assembly’s name, assembly metadata (version, operating system, and others), and public key. |

The information in the assembly manifest can be modified by using the assembly attributes. You can also change the version, information, and attributes of the assembly, such as Trademark, Product, Company, and Copyright.

## Global Assembly Cache

Global Assembly Cache (GAC) is the machine-wide code cache in a computer, which is the centre place for registering assemblies. You should note that the assemblies must be made sharable by registering them in the global assembly cache, only when needed; otherwise, they must be kept private. Moreover, it is not mandatory to install the assemblies in the GAC in order to make them accessible to the Component Object Model (COM) interop or unmanaged code. The COM interop is a service that enables .NET Framework objects to communicate with COM objects.
