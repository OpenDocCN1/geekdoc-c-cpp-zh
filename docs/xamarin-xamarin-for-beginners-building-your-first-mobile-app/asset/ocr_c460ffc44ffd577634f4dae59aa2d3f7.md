and the Visual Studio development environment.

# Different programming interfaces

All previous operating systems rely on different APIs. However, there are some similarities for user-interface objects. For example, all previous systems provide a way for the user to choose a Boolean logical state that can be represented as True or False. In iOS, this object is classified as a view named UISwitch, in Android it is a widget called Switch, and in Windows it is called ToggleSwitch.

# The solution provided by Xamarin

All of the above points can be bypassed by Xamarin because it provides a single programming language, C-Sharp, that can be used to write applications on any operating system. It also provides a single advanced development environment, Visual Studio 2015, for writing these applications (the Xamarin Studio development environment can also be used for Mac). In addition, it unified the various APIs into a single developer interface.

The C-Sharp language is defenseless. It is a strong, flexible, very rich and enduring language. It has truly become one of the most advanced and modern programming languages. We are not here to prefer a programming language over another, but in my personal experience, and to know many other programming languages, you can say that Sea Sharp occupies a prominent position among them.

For a specific application, developers can write one common code for all previous operating systems without any modifications to them in terms of business logic within the application and the software operations that are not related to the type of mobile device or operating system it is running on. We call this code independent of platform independent. If the application is required to handle the hard hardware of the device it is working on (such as a camera or a GPS sensor), then you can write parts of the code that take into account the specificity of each operating system, we call such code as the code associated with the platform dependent operating system.