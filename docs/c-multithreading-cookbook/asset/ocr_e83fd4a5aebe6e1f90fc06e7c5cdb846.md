# Threads in the .NET Framework

Our goal is to have a closer look at one of the most powerful frameworks today—the Microsoft .NET framework. The Microsoft .NET framework provides excellent programming tools such as UI forms, templates, predefined controls, code, SQL Server development tools, with multiple programming languages, such as C#, F#, and Visual Basic. We will focus on the Common Language Runtime (CLR); C++ language, also known as C++/CLI, where CLI stands for Common Language Infrastructure, which is a standard part of the framework.

Since the .NET framework is very large and complex—we will focus on explaining the multithreaded approach and synchronization of objects and techniques.

# Managed versus unmanaged code

You can think of a framework as a set of routines and objects that helps you create an application more easily and with rich content, to a variety of predefined controls and UI objects. When you code, at the end, you need to compile it. After compilation, you often get a compiled (.exe), a dynamic library (.dll), a kernel driver (.sys), and so on. Compiled file (or more files) contains the machine language (code) that consists of zeros and ones and is not readable by humans. This, by definition, is called unmanaged code. So, native C++ (the code that we were coding so far) is compiled directly into the machine language and we call it unmanaged code. Unlike managed code, it is fast and executed directly on Hardware Abstraction Layer (HAL), which provides direct interaction with the machine hardware and low-level execution.

> The HAL refers to a layer of software that deals directly with your computer hardware. The HAL operates at a level between the hardware and the Windows executive services, applications and device drivers need not be aware of any hardware-specific information. It hides hardware-dependent details such as IO interfaces, interrupt controllers, and multiprocessor communication mechanisms. Applications and device drivers are no longer allowed to deal with the hardware directly and must make calls to the HAL routines to determine hardware-specific information (MSDN).

On the other hand, unmanaged code is a bit different. It is executed over common language runtime, or in other layers that reside between the machine hardware and your application. The code you write is not compiled directly into the machine language. It is compiled into an intermediate language, MSIL or Microsoft Intermediate Language. This gives your code advantages and disadvantages.

Let's review the advantages. Managed code, after it is compiled into MSIL, is checked for various errors, as static type checking (which is not performed on native code compilation) and runtime checking. It offers a garbage collector, or the ability to free unused dynamic memory allocated by the application and so on. We already said that the framework provides rich programming tools, which we summarize everything, there are lots of advantages to using the .NET framework.

![](bbox=[0.176, 0.831, 0.213, 0.866])