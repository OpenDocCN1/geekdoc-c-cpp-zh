# From Xcode to Visual Studio

> *A tool is usually more simple than a machine; it is generally used with the hand, whilst a machine is frequently moved by animal or steam power.*
> 
> Charles Babbage

This chapter is all about tools. As much as we might like to think otherwise, developers can’t produce applications without the aid of modern tools such as Xcode, Visual Studio, Eclipse, or any number of other IDEs.

This chapter covers the IDE used for developing iOS applications, Xcode, and the IDE used for building Windows Phone 7 applications, Visual Studio.

Developers need to know some basic things about Visual Studio so that they can move around within that environment smoothly and efficiently and write their applications without the tools getting in their way. In addition to a tour of Visual Studio 2010, I also provide a high-level overview of Xcode and its fundamentals.

# Xcode and iOS Application Development

Xcode is the IDE used by developers for building Mac desktop applications as well as iOS applications. It is an incredibly configurable tool, allowing you to change everything from the window layout, whether it does all of its editing in a single window, the colors, and hundreds of other preferences.

The main output of an Xcode project can be found under the Targets folder. When you use Xcode to build an application, that application is a target. Each target is composed of a bunch of source code files, statically linked libraries, and Frameworks that are referenced as part of the project. For example, if you’re going to build an iOS application that uses Core Data for persisting data on the phone, you’ll have to add `CoreData.framework` to the Frameworks configuration of your Xcode project.