
## Creating a Project in Xcode

Every Cocoa application starts life as a project. A **project** is a repository for all the elements that go into the application, such as source code files, frameworks, libraries, the application’s user interface, sounds, and images. You use the Xcode application to create and manage your project. In this chapter, you will learn to create a project, and see what all the various parts of a project are for. In the process, you will learn how to navigate the Xcode user interface, and you will learn about all the different folders available for you.

### Open Xcode

To open Xcode:

- 1. In the Finder, go to `/Developer/Applications`.
- 2. Double-click the icon, shown in Figure 2-1.

**Figure 2-1** The Xcode application icon

![](img/52b51a77032f3549c0adc4a141b59201_14_0.png)

The first time you start Xcode, it takes you through a quick setup process. The default settings should work for the majority of users.

### Make a New Project

This section will guide you through the process of creating a project. Though it is focused on creating a project suitable for Currency Converter, you will learn about other options available to you when creating a new project.

#### Choose the New Project Command

To create a project, choose File > New Project. The New Project Assistant appears.

#### Choose a Project Type

Xcode can build many different types of applications, including everything from Carbon and Cocoa applications to Mac OS X kernel extensions and Mac OS X frameworks. For this tutorial, use the Cocoa Application template.

- 1. Select Cocoa Application and click Choose…, as shown in Figure 2-2.

**Figure 2-2** The New Project Assistant in Xcode

![](img/52b51a77032f3549c0adc4a141b59201_15_0.png)

- 2. Type the project’s name, Currency Converter, in the save sheet, and choose where you want to save the project. Then click Save.

Xcode creates the project’s files and displays the project window, shown in Figure 2-3.

**Figure 2-3** The new Currency Converter project in Xcode

![](img/52b51a77032f3549c0adc4a141b59201_16_0.png)

### The Xcode Project Interface

The Groups & Files list allows you to easily navigate through your project’s files and targets. All the source files, images, and other resources that make up a project are grouped in the project group, the first item in the Groups & Files list; this group is named after the project (here, Currency Converter). The project’s files are grouped into subgroups, such as Classes, Other Sources, Resources, and so on, as shown in Figure 2-3. Groups are very flexible because they do not necessarily reflect either the on-disk layout of files in the project or the way the build system handles those files. Groups are purely for organizing your project. The groups created by Xcode should be suitable for most developers, but you can customize them however you like.

These are the groups Xcode sets up for Cocoa applications:

- **Classes.** This group holds all the classes required by your application.
- **Other Sources.** This group contains the `main.m` file, which defines the `main` function that runs the application. (You shouldn’t have to modify this file.) It also contains `Currency_Converter_Prefix.pch`. This “prefix header” helps Xcode reduce compilation time. You don’t need to worry about this file.
- **Resources.** This group contains the nib files and other resources that specify the application’s user interface.
- **Frameworks.** This group contains the frameworks (which are similar to libraries) that the application uses.
- **Products.** This group contains the results of project builds and is automatically populated with references to the products created by each target in the project.

Below the project group are other groups, including smart groups. **Smart groups**—identified by the purple folders on the left side of the list—allow you to access the project’s files using custom rules in a way similar to using smart playlists in iTunes.

These are some of the other groups in the Groups & Files list:

- **Targets.** This group lists the end results of your builds. This group usually contains one target, such as an application or a framework, but it can consist of multiple items.
- **Executables.** This group contains the executable products your project creates.
- **Errors and Warnings.** This group displays the errors and warnings encountered in your project when you perform a build.

Curious folks might want to look in the project directory in Finder to see the files it contains. Among the project files are:

- `Currency Converter.xcodeproj`  
  This package contains information that defines the project. You should not modify it directly. You can open your project by double-clicking this package.
- `main.m`  
  An Objective-C file, generated for each project, that contains the `main` function of the application.
- `English.lproj`  
  A directory containing resources localized to the English language. In this directory are nib files automatically created for the project. You may find other localized resource directories, such as `Dutch.lproj`.

### What’s Next?

In this chapter, you made an Xcode project that will contain all the resource files for a Cocoa application. In the next chapter, you will learn how to create the model, the basic functionality behind an application.

## Defining the Model

Model objects contain special knowledge and expertise. They hold data and define the logic that manipulates that data. For example, a customer object, common in business applications, is a model object. In Currency Converter, the model class you’re going to create is the converter class. In the MVC design pattern, instances of a model class do not communicate directly with the user interface.

In this chapter, you will create the model for your application. First, you will learn how to create a new class in Xcode. Then, you will define the interface for your model before implementing it. Finally, you will implement the entire functionality of the class. In the process, you will learn some of the syntax of Objective-C, including how to declare variables and methods. You will also be introduced to the concept of declared properties—a feature in Objective-C 2.0 that makes writing accessor methods incredibly quick and simple.

### Specify the Model Class

- 1. Select the Classes group in the Groups & Files list.
- 2. Choose File > New File.
- 3. Select Objective-C class in the Cocoa Class group. Leave it as a subclass of NSObject, and click Next.

![](img/52b51a77032f3549c0adc4a141b59201_18_0.png)

Objective-C 2.0 provides a feature called **declared properties**. A property declaration is, effectively, a shorthand for declaring the setter and getter for an attribute of an instance of a class. In addition to the declaration itself, there are directives to instruct the compiler to synthesize the accessors and to inform the compiler that you will provide the methods yourself at runtime. There are two parts to a property, its declaration and its implementation.

You declare a property as follows:

```
@property(attributes) Type variableNameList;
```

where *attributes* is a comma-separated list of keywords such as *readwrite* and *copy*, for example:

```
@property(copy) NSString *name;
```

Your converter class wants to provide access to its data to external objects, so you need to declare accessor methods.

- 1. Place your insertion point after the closing brace of the instance method declarations in `Converter.h`, just before the `@end` directive.
- 2. Add the following property declaration for your two instance variables.

  `@property(readwrite) float sourceCurrencyAmount, rate;`

At compile time, the compiler treats this as if you had declared the following methods:

```objc
- (float)sourceCurrencyAmount;
- (void)setSourceCurrencyAmount:(float)newSourceCurrencyAmount;
- (float)rate;
- (void)setRate:(float)newRate;
```

The property declaration simply declares what the accessor methods will look like. In the next section, you will provide an implementation for the accessor methods.

### Declare the Model Method: convertCurrency

The one method the model requires is a simple function to multiply the two values encapsulated by the converter class.

Add the following line as the next line of code in `Converter.h`:

```objc
- (float)convertCurrency;
```

Although this method takes no arguments, it nonetheless provides the result of multiplying the source currency amount with the conversion rate. This is possible because instance methods have access to the instance variables of their object. At runtime, the instance method treats all instance variables as if they were local variables. It is common practice to use accessor methods even when the variable is in scope. This practice makes it clear that the code is accessing an instance variable, rather than a local variable.
