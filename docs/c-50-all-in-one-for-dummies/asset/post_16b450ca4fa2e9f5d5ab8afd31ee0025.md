
# 564 Using Some of the T4 Directives

- **culture**: This sets the System.Globalization culture. You know, like en-US or en-GB.
- **debug**: Just like the ASP.NET debugger, this sets the return of debug symbols.
- **hostspecific**: This is for use custom hosts — you'll run it if you are writing for custom hosts.

# Including includes

Includes are nice and easy.

Remember ASP classic? No, I don't mean ASP.NET-MVC. I mean the old ASP, with VB script, pre-.NET. This is like that. (If you don't, that's okay; I explain it in the next section.)

If you want to include the contents of a file somewhere in your template, drop the `include` directive there and the name of the file in a file attribute.

```xml
## include file="c:\specialsource.cs" #
```

That's all there is to.

# Importing items and assemblies

The `import` and `assembly` directives assist with writing code in a template. In the example in the previous section, I emitted text, but in the real examples that you find in MSDN, you write C# or VB code to modify the text.

If you want to use .NET Framework constructs, you need to reference the `assembly` and `import` the namespace. For instance, if you are going to get values from a file in your template, you need the `System.IO` library.

First you need to reference the `assembly` unless you are certain it will be referenced in the project. You should `import` the namespace so that you don't have to reference items via fully qualified names, like this:

```xml
## assembly name="System.IO.DLL" #
## import namespace="System.IO" #
```

Then, you can reference the file maintenance classes inside the code of the template. You reference code using the `<#` and `# >` statements.

# Book V

# Windows Development with WPF

![](img/6df7bb88e9302e98442acc219cfbd7fc_590_0.png)

Basic Input Controls

# Contents at a Glance

- Chapter 1: Introducing WPF ................................................................................................................567
- Chapter 2: Understanding the Basics of WPF ..........................................................................................................577
- Chapter 3: Data Binding in WPF ......................................................................................................................................601
- Chapter 4: Practical WPF ......................................................................................................................................................................623

# Chapter 1: Introducing WPF

## In This Chapter

- Taking a first look at WPF and what it can do for you
- Working with XAML
- Building your first WPF application
- Comparing XAML to C#

WPF, or Windows Presentation Foundation, is a graphical system for rendering user interfaces. It provides great flexibility in how you lay out and interact with your applications. With Common Language Runtime (CLR) of its core, you can use C# or any other CLR language to communicate with user interfaces and develop application logic. The advantages of WPF for your application are its rich data binding and visualization support and its design flexibility and styling.

WPF enables you to create an application that is more usable than your audience. It gives you the power to design an application that would previously take extremely long development cycles and a calculus genius to implement. Now you can implement difficult things like graphics and animations in as few as three lines of code!

This chapter introduces you to key WPF concepts as well as common application patterns used in the software industry today.

## Understanding What WPF Can Do

WPF's graphics capabilities make it the perfect choice for data visualization. Take, for instance, the drop-down list (or combo box). Its current use is to enable the user to choose a single item from list of items. For example, suppose you want the user to select a car model for purchase.

The standard way of displaying this choice is to display a drop-down list of car model names from which users can choose. There is a fundamental usability problem with this common solution: Users are given only a single piece of information from which to base their decision — the text that is used to represent the item in the list.

For the power user (or fanatic), this may not be an issue, but other users need more than just a model name to make an educated decision on the car they wish to purchase. This is where WPF and its data visualization capabilities come into play.

A template can be provided to define how each item in the drop-down list is rendered. The template can contain any visual element, such as images, labels, text boxes, tooltips, drop shadows, and more!

Figure 1-1 shows a typical display of a combo box. This control has limits to the user only a single piece of information, the text used to represent the car model. Work can be done to display images of the car models in a separate control based on the selection in the list, but this still mandates users to make their selection before seeing what it is choosing. In contrast, WPF has the flexibility to display many pieces of information in each combo box item, like a one-stop shop for all the information user will need to make their decision. (See Figure 1-2 for a WPF combo box.)

![](img/6df7bb88e9302e98442acc219cfbd7fc_593_0.png)

Figure 1-1: A typical combo box.

Figure 1-2 shows a sample combo box in WPF. The way the combo box item is rendered is defined using a data template. (Cover Data Templates in Chapter 3 of this book.) Each item in this combo box is rendered to provide a visual cue along with multiple data fields. Displaying all this information enables users to make an educated decision about the choice they are making.

![](img/6df7bb88e9302e98442acc219cfbd7fc_593_1.png)

Figure 1-2: Visualizing data — a WPF combo box.

# Diving In! Creating Your First WPF Application

## Introducing XAML

WPF enables you to build user interfaces declaratively. XAML (hint: rhymes with camel) forms the foundation of WPF. XAML is similar to HTML in the sense that interface elements are defined using a tag-based syntax.

![](img/6df7bb88e9302e98442acc219cfbd7fc_594_0.png)

XAML is XML-based, and as such, it must be well formed, meaning all opening tags require closing tags, and all elements and attributes contained in the document must validate against the specified schemas.

By default, when creating a WPF application in Visual Studio 2012, the schemas are represented in XAML files:

- http://schemas.microsoft.com/winfx/2006/xaml/presentation: This schema represents the default Windows Presentation Framework namespace.
- http://schemas.microsoft.com/winfx/2006/xaml/schema: This schema represents a set of classes that map to CLR objects.

Most CLR objects can be expressed as XAML elements (with the exception of abstract base classes and other nonabstract base classes used strictly for inheritance purposes in the CL). XAML elements are mapped to classes; attributes are mapped to properties or events.

At runtime when a XAML element is processed, the default constructor for its underlying class is called, and the object is instantiated; its properties and events are set based on the attribute values specified in XAML.

I am a firm believer that the best way to become comfortable with WPF and XAML is to jump right in and give it a try. The next sections review more XAML basics and get you started on the path of WPF application development.

# In! Creating Your First WPF Application

Now it's time to get comfortable, stop for a moment, grab a caffeinated beverage, sit in a comfortable chair, pull up to your computer, and get ready to go!

To create your first project, follow these steps:

1. Open Visual Studio 2012.
2. Create a new project by choosing File:New Project.
