
## Programming in C#

- (f) In C#, all data types are treated as objects.
- (g) Class definition of C# is identical to the class definition of C++.
- (h) Like C++, C# supports multiple code inheritance.
- (i) Array declarations in C# are identical to Java array declarations.
- (j) C# was first officially announced by Microsoft in 2000.

- 1.2 State at least five most important highlights of C# language.
- 1.3 What are the shortcomings of C++ language? List at least five of them.
- 1.4 What are the features of Java which have been implemented in C#?
- 1.5 How is C# better than Java?
- 1.6 What are the limitations of using the Internet today?
- 1.7 What is the primary motivation of Microsoft Corporation in developing C# language?
- 1.8 C# is a modern language. Comment.
- 1.9 Why is C# called type-safe language?
- 1.10 State ten significant differences between C# and C++.
- 1.11 State ten significant differences between C# and Java.
- 1.12 State five features of C++ that have not been incorporated into C#.
- 1.13 State some of the new features that are unique to C# language.
- 1.14 Explain the need for Virtual Object System (VOS) in C#.

## 2 Understanding .NET: The C# Environment

### 2.1 THE .NET STRATEGY

We briefly discussed in the previous chapter how C# was created as a language for developing systems for the .NET platform. As pointed out, Microsoft wanted to make the World Wide Web (WWW) more vibrant by enabling individual devices, computers and web services to work together intelligently to provide richer solutions to users. By the intelligent integration of web sites on the Internet, users can create a wide variety of value-based applications such as unified banking services, electronic bill payment, stock trading, insurance services and comprehensive supply chain management. Microsoft calls this ‘Web services’ and the software strategy for implementing and delivering these services is ‘.NET’.

.NET is a software framework that includes everything required for developing software for web services. It integrates presentation technologies, component technologies and data technologies on a single platform so as to enable users to develop Internet applications as easily as they do on desktop systems. Microsoft took many of the best ideas in the industry, added their own creativity and innovations and produced a coherent systems solution popularly known as Microsoft .NET. The Microsoft .NET software solution strategy includes three key approaches as shown in Fig. 2.1.

Microsoft .NET platform includes the following components that would help develop a new generation of smart Internet services:

- .NET infrastructure and tools
- .NET user experience
- .NET building block
- .NET device software

Microsoft .NET products and services consist of the following:

- Windows .NET
- MSN .NET
- Office .NET
- Visual Studio .NET
- Personal subscription services
- bCentral for .NET

![](img/bae4ee2c7c29c052feb3b9a9c5659998_28_0.png)

Third-party .NET services will provide opportunities to a vast range of developers and users to produce corporate and vertical services using .NET platform.

### 2.2 THE ORIGINS OF .NET TECHNOLOGY

Before going into the details of .NET features further, we shall see how the concept of .NET was evolved over the past ten years. The current technology of .NET has gone through three significant phases of development:

- OLE technology
- COM technology
- .NET technology

These developments that took place during the 1990s are illustrated in Fig. 2.2.

![](img/bae4ee2c7c29c052feb3b9a9c5659998_29_0.png)

#### 2.2.1 OLE Technology

OLE (Object Linking and Embedding) technology was developed by Microsoft in the early 1990s to enable easy interprocess communications. OLE provided support to achieve the following:

- To embed documents from one application into another application
- To enable one application to manipulate objects located in another application

This enabled users to develop applications which required inter-operability between various products such as MS Word and MS Excel.

#### 2.2.2 COM Technology

Till the advent of COM technology, the monolithic approach had been used for developing software. But when programs become too large and complex, the monolithic approach leads to a number of problems in terms of maintainability and testing of software. To overcome these problems, Microsoft introduced the component-based model for developing software programs. In the component-based approach, a program is broken into a number of independent components where each one offers a particular service. Each component can be developed and tested independently and then integrated it into the main system. This technology is known as the Component Object Model (COM) and the software built using COM is referred to as componentware.

COM technology offers a number of benefits to developers and users. It

- reduces the overall complexity of software
- enables distributed development across multiple organizations or departments and
- enhances software maintainability

#### 2.2.3 .NET Technology

.NET technology is a third-generation component model. This provides a new level of interoperability compared to COM technology. COM provides a standard binary mechanism for intermodule communication. This mechanism is replaced by an intermediate language called Microsoft Intermediate Language (MSIL) or simply IL in the .NET technology. Various .NET-language compilers

- Compilation of IL into native executable code
- Providing metadata
- Memory management (automatic garbage collection)
- Enforcement of security
- Interoperability with other systems
- Managing exceptions and errors
- Support for tasks such as debugging and profiling

Figure 2.6 shows a flow chart of CLR activities that go on when an application is executed. The source code is compiled to IL while the metadata engine creates metadata information. IL and metadata are linked with other native code if required and the resultant IL code is saved. During execution, the IL code and any requirement from the base class library are brought together by the class loader. The combined code is tested for type-safety and then compiled by the JIT compiler to produce native machine code, which is sent to the runtime manager for execution.

#### 2.4.1 Common Type System (CTS)

The .NET Framework provides multiple language support using the feature known as Common Type System that is built into the CLR. The CTS supports a variety of types and operations found in most programming languages and therefore calling one language from another does not require type conversions. Although C# is specially designed for the .NET platform, we can build .NET programs in a number of other languages including C++ and Visual Basic.

#### 2.4.2 Common Language Specification (CLS)

The Common Language Specification defines a set of rules that enables interoperability on the .NET platform. These rules serve as a guide to third-party compiler designers and library builders. The CLS is a subset of CTS and therefore the languages supporting the CLS can use each others' class libraries as if they are their own. Application Program Interfaces (APIs) that are designed following the rules of CLS can easily be used by all the .NET languages.

#### 2.4.3 Microsoft Intermediate Language (MSIL)

MSIL, or simply IL, is an instruction set into which all the .NET programs are compiled. It is akin to assembly language and contains instructions for loading, storing, initializing and calling methods. When we compile a C# program or any program written in a CLS-compliant language, the source code is compiled into MSIL.

![](img/bae4ee2c7c29c052feb3b9a9c5659998_31_0.png)

Fig. 2.5 Component of CLR

![](img/bae4ee2c7c29c052feb3b9a9c5659998_31_1.png)

Fig. 2.6 Flowchart of CLR activities for executing a program
