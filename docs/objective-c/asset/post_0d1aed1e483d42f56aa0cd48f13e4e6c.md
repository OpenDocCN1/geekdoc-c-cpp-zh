
provides the classes needed for building GUI applications on iPhone and iPad, and a slew of other frameworks which provide functionality specific to things such as network services, graphics, and so on. For the purposes of this book, we will focus exclusively on Foundation. This framework easily has the greatest cross-platform support of any of the frameworks on MacOS X. It is available in the official Apple versions on MacOS X, iPhone, and iPad, and in the form of open source third-party implementations on Linux, BSD UNIX, and even Windows. One type of implementation enables you to develop your application by using Xcode on MacOS X, and cross compile to build an executable for Windows. In many ways, the Foundation framework provides greater portability and power than some standard libraries that have been built specifically for that purpose.

For now, however, since Apple platforms are by far the most popular platforms for Objective-C developers at this time, I focus primarily on features available there.

## Using Frameworks in Your Projects

Though it is specific to MacOS X, I am going to visit, briefly, the subject of using frameworks in your own projects so that you’ll know how to handle them when you need to.

Frameworks provided by Apple are typically installed in the directory that you installed Xcode, by default /Developer. Under this directory, you’ll find a directory called Platforms. Inside the Platforms directory, you’ll find a directory for each of the different development platforms for which you have an SDK installed. For example, if you have installed the iPhone SDK, then you will see directories corresponding to iPhone OS. If you have not, then you will only see directories corresponding to MacOS X.

Inside of the SDK directory, you’ll find a path leading to System/Library/Frameworks It is within this directory that all of the frameworks for this particular platform in this particular SDK located.

## Adding frameworks

Adding a framework to your project is very straightforward. You simply right-click or option click the target to which you intend to add the framework, and choose Add ⇧ Existing Frameworks. Doing this brings up the framework selection dialog box, as shown in Figure 11.1.

This dialog box enables you to select from the list of installed frameworks whichever framework you wish to link with your currently selected target.

Figure 11.1

The framework selection dialog box.

- AGL.framework
- Accelerate.framework
- AddressBook.framework
- AppKit.framework
- AppKitScripting.framework
- AppleScriptKit.framework
- AppleScriptObjC.framework
- AppleShareClientCore.framework
- ApplicationServices.framework
- AudioToolbox.framework
- AudioUnit.framework
- Automator.framework
- CP437.dylib
- CP850.dylib
- CalendarStore.framework
- Carbon.framework
- Cocoa.framework
- Collaboration.framework
- CoreAudio.framework
- CoreAudioKit.framework
- CoreData.framework
- CoreFoundation.framework
- CoreLocation.framework

All

Name

Add Other...

Cancel

## Including the headers

Remember that simply linking with the framework is not enough to enable you to actually use the classes and code contained within it. You also need to be sure to include the appropriate header files into your source file. Recall when you learned about importing header files that you tell the compiler to search the linked framework directories by enclosing the name of the header file you are importing in <>. Doing so causes the compiler to search the system including directories as well as any framework directories.

## Considering garbage collection

An important consideration when linking with third-party frameworks is to ensure that the framework in question supports the memory management model that you have selected for your project. Not all frameworks support both garbage collection and reference counted memory management. So be sure when you are reviewing the documentation for the framework that you intend to link to your project that you are linking with the correct version of that framework for the memory management system that you have selected. Linking with the incorrect version will cause a compilation error.

## Summary

In this chapter, I have introduced you to the concept of frameworks and also talked about the Foundation framework which serves as the closest thing to a standard library that Objective-C has. The remainder of this part of the book will utilize the Foundation framework extensively and it is important that you have this conceptual introduction to the framework and what it provides. Now that you have this background information, you’ll be better prepared for the detailed coding examples to come.

## Using Strings

Any good standard library needs a great string class, and Objective-C with Foundation is no exception. In fact, the foundation framework comes with an excellent string class, NSString. Like many of the low-level core classes in Foundation, an immutable version of NSString, as well as a mutable version called NSMutableString exists. These two classes give you a tremendous amount of functionality when working with string values.

## Understanding the String Declaration Syntax

Although NSString and NSMutableString have many types of initializers and factory methods available, strings are such a commonly used class in Objective-C, a special language construct has been created explicitly for the purposes of declaring a string easily. This construct is shown in Listing 12.1.

### Listing 12.1
### The Objective-C NSString shortcut syntax

```
NSString *someString = @"this is a string";
```

Essentially, the compiler knows that any time it encounters @ and then a string contained within double quotes, it should create a static const NSString object to contain the string provided.

Any two declarations of the exact same string value, even if stored in different variable names, point to the same object. Therefore, you can use these strings for keys, for example, where the equality of the string as compared to another instance of that string will be considered to be equal, both using the -isEqual: object method as well as the == operator, which will compare the value of the pointers.

## In This Chapter

- Using the NSString and NSMutableString Classes
- Understanding Format Strings
- Using the Special Objective-C String Declaration Syntax

To illustrate this, look at Listing 12.2.

### Listing 12.2
### Examining string constant equality

```
NSString *string1 = @"this is a string";
NSString *string2 = @"this is a string"; // same object as string1
NSString *string3 = [NSString stringWithString:string1]; // makes new

assert(string1 == string2); // true
assert([string1 isEqual:string2]); // also true
assert([string1 isEqual:string3]); // true
assert(string1 == string3); // false
```

Most often, you declare strings using the Objective-C string construct, but numerous initializers and factory methods are available on the NSString and NSMutableString classes. Some of the more common ones are shown in Table 12.1.

### Table 12.1 NSString and NSMutableString factory methods.

| Method | Purpose |
|---|---|
| +string | Constructs a new empty string. |
| +stringWithFormat: | Constructs a new string using the printf-style format specifier given and any arguments required by the format specifier. |
| +stringWithCharacters:length: | Constructs a new string containing length characters retrieved from the C. style array provided. |
| +stringWithString: | Constructs a new string with the value of the given string. |
| +stringWithCString:encoding: | Constructs a new string using a C. style string by converting it using the specified encoding. |
| +stringWithUTF8String: | Constructs a new string using a C.-style string encoded with UTF-8 string encoding. This is equivalent to calling +stringWithCString:encoding: using NSUTF8Encoding for the encoding parameter. |
| +stringWithContentsOfFile:encoding:error: | Constructs a new string containing the contents of the file specified using the encoding provided. |
