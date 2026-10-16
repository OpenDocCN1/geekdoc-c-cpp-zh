# 26 Composition



+   • Architecture of the Composition Framework
+   • Composition using attributes
+   • Convention-based registration
+   • Contracts
+   • Exports and imports of parts
+   • Containers used by hosting applications
+   • Lazy loading of parts



The wrox.com code downloads for this chapter are found at www.wrox.com/go/professionalssharp6 on the Download Code tab. The code for this chapter is divided into the following major examples:

+   • Attribute-Based Sample
+   • Convention-Based Sample
+   • UI Calculator (WPF and UWP)



Microsoft Composition is a framework for creating independency between parts and containers. Parts can be used from containers without the need for the container to know the implementation or other details. The container just needs a contract—for example, an interface to use a part.

Microsoft Composition can be used with different scenarios, such as a dependency injection container, or you can even use it for adding functionality to an application after the application is released by dynamically loading add-ins into the application. To get into these scenarios, you need a foundation.

For making development of apps easier, it’s a good practice to have separation of concerns (SoC). SoC is a design principle for separating a program into different sections where each section has its own responsibility. Having different sections allows you to reuse and update these sections independently of each other.

Having a tight coupling between these sections or components makes it hard to reuse and update these components independently of each other. Low coupling—for example, by using interfaces—helps this goal