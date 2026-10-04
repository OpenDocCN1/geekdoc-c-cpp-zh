
# 5

# Programming Your ASP.NET Web Pages

WHAT WILL YOU LEARN IN THIS CHAPTER:

- How to work with data types, variables, objects, and collections in a programming environment
- Different ways to make decisions in your code
- The options available for creating blocks of functionality that can easily be reused
- Different ways to write well-organized and documented code
- What object orientation is, and how you can use it in your applications

WROX CODE DOWNLOADS FOR THIS CHAPTER

You can find the wrox.com code downloads for this chapter on the Download Code tab at www.wrox.com/go/begaspnet451. The code is in the Chapter 5 folder.

In the previous four chapters, you created a number of Web Forms that contained mostly ASP.NET Server Controls and created HTML. Only a few of the examples contained actual programming code, written in either C# or Visual Basic (VB.NET), and most of that code was pretty straightforward. However, not all of your pages will always be simple, and the ability to read, understand, and write code is a critical asset in your web development toolkit.

This chapter teaches you the basics and beyond of programming for web applications. Just as all the other samples in the book, this entire chapter covers both VB.NET and C#. For every concept or piece of theory introduced in this chapter, you will see an example in both VB.NET and C# at the same time. Which language you prefer is entirely your decision.

## 16 | CHAPTER 5 PROGRAMMING YOUR ASP.NET WEB PAGES

> NOTE To get the most out of this chapter, it's recommended that you actually try the code. You can test the examples with a simple ASPX page. Draw a Label and a Button on your page and double-click the Button in Design View. Then type the sample code on the open line of the code block that VS added for you and press Ctrl+F5. After the page has finished loading, click the button and the code will be executed. Some of the examples call fictitious code won't run correctly. They only serve to illustrate the topic being discussed.

## INTRODUCTION TO PROGRAMMING

To get started with programming, it's critical to understand a common set of terms shared by programmers in all types of languages and applications. The remainder of this chapter introduces a relatively large number of terms and concepts. Most of the terminology comes with code examples you can see how they are used in real code.

It's also important to realize that this is not a complete introduction to programming. Not every detail of a programming language is covered. Instead, this chapter focuses on the key concepts that you need to understand to successfully build day-to-day websites. Once you get the hang of that you'll find easier to deepen your knowledge about programming by learning the more exotic features of your favorite language.

> If you're interested in learning a lot more about programming in VB.NET or C#, find Beginning Visual Basic 2012 (Bryan Newsome, 2012; ISBN: 978-1183-1181-3) or Beginning Microsoft C# 2012 (Karli Watson et al., 2012; ISBN: 978-1183-1441-8), both published by Wrox.

Add the code you write in this and all coming chapters either to the Code Behind of a web page, or in a separate class file placed in the special folder. When the ASP.NET run time processes the request for a page containing code, it compiles any code it finds in page, Code Behind, or class files. When code is compiled, it is transformed from a human-readable language (like C# or VB.NET) into Microsoft Intermediate Language (MSIL), the language that the .NET Framework can understand and execute. The result of the compilation of an ASP.NET website is one or more files—with a DLL extension—in a temporary folder on your system. This compilation process takes place the first time the page is requested after it has been created or changed. Fortunately, subsequent requests to the same page result in the DLL being reused for the request. In ASP.NET websites, compilation takes place behind the scenes, so you usually don't have to worry about it.

To get started with programming, the first concepts that you need to look at are data types and variables, because they are the building blocks of any programming language.

> NOTE The .NET Framework used by ASP.NET is huge and contains thousands of types with hundreds of thousands of members. Clearly, you cannot memorize all the types in the framework, so you need to make good use of resources like IntelliSense and online help. Navigating MSDN site (http://msdn.microsoft.com/en-us/library/) can sometimes be a daunting task. However, I find that searching for something like typeName brings exactly what I need. So, if I wanted to learn more about the string class, I would type string class .NET MSDN in my favorite search engine. Nine out of ten times the first result is a link to the relevant page on the MSDN website, where I can learn more about the class — where it's defined and how to use it.

## DATA TYPES AND VARIABLES

At first when you think about data that is used in some programming environment, you may not realize that each piece of data has a data type. You may think that a computer would store the text Hello World in exactly the same way as today's date or the number 26; as a series of characters, for example. However, to able to effectively work with data, many programming languages use different types, and each data type is constrained to a specific type of information. Out of the box, the .NET Framework comes with a list of data types that enable you to work with numbers (as Int32, Int16 and Double), text strings (Char and String), dates (DateTime), true/false constructs (Boolean), and a List of the most common types is supplied later in this section.

For each type of data there is a specific type to work. With that data, you can store in a variable that you need to declare the required data type. In VB.NET you use Dim myVariable As DataType, whereas in C# you use dataType myVariable to declare a variable. A valid variable name consists of letters, numbers, and underscores, and cannot start with a number. These rules apply to other identifiers as well, as classes and methods, which you see later. The following example shows how to declare two variables: an Integer (int in C#) to hold a number and a String (string in C#) to hold a piece of text:

### VB.NET

' Declare a variable of type Integer to hold medium sized whole numbers.
Dim distanceInMiles As Integer
' Declare a variable to hold some text like a first name.
Dim firstName As String

### C#

// Declare a variable of type int to hold medium sized whole numbers.
int distanceInMiles;

// Declare a variable to hold some text like a first name.
string firstName;

These two code examples also contain comments, prefixed with a tick (') in VB.NET or two forward slashes (//) in C#. You learn more about commenting your code later in this chapter.

After you have declared a variable, you can assign it a value. You can assign types like numbers and booleans to a variable. To assign a string to a variable you need to enclose it in double quotes:

### VB.NET

Dim distanceInMiles As Integer
distanceInMiles = 437

Dim firstName As String
firstName = "Imar"

### C#

int distanceInMiles;
distanceInMiles = 437;

string firstName;
firstName = "Imar";

In addition to separate declarations and assignments, you can also declare a variable and assign it a value in one sweep:

### VB.NET

Dim distanceInMiles = 437
Dim firstName = "Imar"

### C#

int distanceInMiles = 437;
string firstName = "Imar";

Although a variable name can be anything you like, it's advised that you give each variable a meaningful name that describes its purpose. For example, a string to hold a firstName and a variable that holds someone's age could be called age. In .NET's common to write local variables in a case called camelCase, which means each word starts with a capital letter except for the first. For example, you find the type of the variable later in the code, VS shows a useful tooltip when you hover over a variable in the code editor, making it easy to find a variable's type. Figure 5-1 shows that the distanceInMiles variable in the C# example is of int.

```
int distanceInMiles;
distanceInMiles = 437;
// (local variable) int distanceInMiles
firstName = "Imar";
```

FIGURE 5-1

You're advised not to prefix your variables with letters to indicate the type. For example, write firstName and not FirstName for a String holding someone's name. This type of notation, called Hungarian Notation, is considered outdated. IDEs like Visual Studio, with their IntelliSense and other programming tools, don't really require this anymore. Without Hungarian Notation, your code becomes easier to read (age is more readable than iAge) and easier to maintain because you can change a variable's type without renaming it everywhere it's used.
