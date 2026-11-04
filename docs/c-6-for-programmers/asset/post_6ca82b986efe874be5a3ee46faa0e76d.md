
![](img/3f5ef6be1748bb746e5f71a483bba4d0_83_0.png)

**Fig. 3.4** | IDE with an open console app’s code displayed in the editor and the project’s contents shown in the **Solution Explorer** at the IDE’s top-right side.

The code coloring scheme used by the IDE is called syntax-color highlighting and helps you visually differentiate code elements. For example, keywords appear in blue and comments appear in green. We style our code similarly as discussed in the Preface. One example of a literal is the string passed to Console.WriteLine in line 10 of Fig. 3.1. You can customize the colors shown in the code editor by selecting Tools > Options.... This displays the Options dialog. Then expand the Environment node and select Fonts and Colors. Here you can change the colors for various code elements. Visual Studio provides many ways to personalize your coding experience.

### 3.3.2 Changing the Name of the App File

For the apps we create in this book, we change the source-code file’s default name (Program.cs) to a more descriptive name. To rename the file, right-click Program.cs in the Solution Explorer and select Rename to make the file name editable. Windows automatically selects the file name’s base part (i.e., Program). Type Welcome1, then press Enter to change the name to Welcome1.cs. Be sure to keep the .cs filename extension.

> **Error-Prevention Tip 3.4**
> *When changing a file name in a Visual Studio project, always do so in Visual Studio. Changing file names outside the IDE can break the project and prevent it from executing.*

### 3.3.3 Writing Code and Using IntelliSense

In the editor window (Fig. 3.4), replace the generated code with Fig. 3.1's code. As you begin typing the name Console (line 10), an IntelliSense window is displayed (Fig. 3.5).

a) IntelliSense window displayed as you type

![](img/3f5ef6be1748bb746e5f71a483bba4d0_84_0.png)

Closest match is highlighted

Tool tip describes highlighted item

Fig. 3.5 | IntelliSense window as you type "Con".

As you type, IntelliSense lists various items that start with or contain the letters you've typed so far. IntelliSense also displays a tool tip containing a description of the first matching item. You can either type the complete item name (e.g., Console), double-click the item name in the member list or press the Tab key to complete the name. Once the complete name is provided, the IntelliSense window closes. While the IntelliSense window is displayed, pressing the Ctrl key makes the window transparent so you can see the code behind the window.

When you type the dot (.) after Console, the IntelliSense window reappears and initially shows only class Console's members that can be used on the right of the dot—as you type, this list narrows to items containing what you've typed so far. Figure 3.6 shows the IntelliSense window narrowed down to only items that contain "Write". You also can type "wL" to find all items containing the capital letters "W" and "L" (such as WriteLine).

When you type the opening parenthesis character, (, after Console.WriteLine, the Parameter Info window is displayed (Fig. 3.7). This contains information about the method's parameters—the data that methods require to perform their tasks. As you'll learn in Chapter 7, a method can have several versions. That is, a class can define several methods that have the same name, as long as they have different numbers and/or types of parameters—a concept known as overloaded methods. These methods normally all perform similar tasks.

## 文档结构测试样例

本文档用于测试文档解析系统的各项功能，包含标题、段落、列表、表格、插图和引用等多种元素。通过解析此样例，可以验证解析器对文档结构的识别能力。

- 支持文本检测
- 支持版面分析
- 支持结构化提取

| 序号 | 内容 | 结果 |
| --- | --- | --- |
| 1 | 标题识别 | 通过 |
| 2 | 段落识别 | 通过 |
| 3 | 表格识别 | 通过 |

![](img/3f5ef6be1748bb746e5f71a483bba4d0_85_0.png)

> 这是一条引用文本，用于测试引用块的识别与提取效果。

key, or simply keep typing and ignore it. After you type the app’s code, select File > Save All to save the project.

### 3.3.4 Compiling and Running the App

You’re now ready to compile and execute your app. Depending on the project’s type, the compiler may compile the code into files with the .exe (executable) extension, the .dll (dynamically linked library) extension or one of several other extensions—you can find these files in project’s subfolders on disk. Such files are called assemblies and are the packaging units for compiled C# code. These assemblies contain the Microsoft Intermediate Language (MSIL; Section 1.4.2) code for the app.

To compile the app, select Build > Build Solution. If the app contains no compile-time errors, this will compile your app and build it into an executable file (named Welcome.exe, in one of the project’s subdirectories). To execute it, type Ctrl + F5, which invokes the Main method (Fig. 3.1). If you attempt to run the app before building it, the IDE will build the app first, then run it only if there are no compilation errors. The statement in line 10 of Main displays `Welcome to C# Programming!`. Figure 3.8 shows the results of executing this app, displayed in a console (Command Prompt) window. Leave the app’s project open in Visual Studio; we’ll go back to it later in this section. [Note: The console window normally has a black background and white text. We reconfigured it to have a white background and black text for readability. If you’d like to do this, right-click anywhere in the Command Prompt window’s title bar, then select Properties. You can change the colors in the Colors tab of the dialog that appears.]

![](img/3f5ef6be1748bb746e5f71a483bba4d0_86_0.png)

Fig. 3.8 | Executing the app shown in Fig. 3.1.

### 3.3.5 Errors, Error Messages and the Error List Window

Go back to the app in Visual Studio. As you type code, the IDE responds either by applying syntax-color highlighting or by generating an error. When an error occurs, the IDE underlines the error’s location with a red squiggly line and provides a description of it in the Error List window (Fig. 3.9). If the Error List window is not visible, select View > Error List to display it. In Fig. 3.9, we intentionally omitted the semicolon at the end of line 10. The error message indicates that the semicolon is missing. You can double-click an error message in the Error List to jump to the error’s location in the code.

> **Error-Prevention Tip 3.5**
> One compile-time error can lead to multiple entries in the Error List window. Each error you correct could eliminate several subsequent error messages when you recompile your app. So when you see an error you know how to fix, correct it—the IDE will recompile your code in the background, so fixing an error may make several other errors disappear.

Intentionally omitted semicolon (syntax error)

![](img/3f5ef6be1748bb746e5f71a483bba4d0_87_0.png)

Fig. 3.9 | Syntax error indicated by the IDE.

## 3.4 Modifying Your Simple C# App

This section continues our introduction to C# programming with two examples that modify the example of Fig. 3.1.

### 3.4.1 Displaying a Single Line of Text with Multiple Statements

Class Welcome2, shown in Fig. 3.10, uses two statements to produce the same output as that shown in Fig. 3.1. From this point forward, we highlight the new and key features in each code listing, as shown in lines 10–11 of Fig. 3.10.

```csharp
// Fig. 3.10: Welcome2.cs
// Displaying one line of text with multiple statements.
using System;

class Welcome2
{
7  // Main method begins execution of C# app
8  static void Main()
9  {
10     Console.Write("Welcome to ");
11     Console.WriteLine("C# Programming!");
12 } // end Main
13 } // end class Welcome2
```

Fig. 3.10 | Displaying one line of text with multiple statements.

Welcome to C# Programming!

The app is almost identical to Fig. 3.1. We discuss the changes here. Line 2

```csharp
// Displaying one line of text with multiple statements.
```

states the purpose of this app. Line 5 begins the Welcome2 class declaration.

Lines 10–11 of method Main

```csharp
Console.Write("Welcome to ");
Console.WriteLine("C# Programming!");
```

display one line of text in the console window. The first statement uses Console’s method Write to display a string. Unlike WriteLine, after displaying its argument, Write does not position the screen cursor at the beginning of the next line in the console window—the next character the app displays will appear immediately after the last character that Write displays. Thus, line 11 positions the first character in its argument (the letter “C”) immediately after the last character that line 10 displays (the space character before the string’s closing double-quote character). Each Write or WriteLine statement resumes displaying characters from where the last Write or WriteLine statement displayed its last character.

### 3.4.2 Displaying Multiple Lines of Text with a Single Statement

A single statement can display multiple lines by using newline characters, which indicate to Console methods Write and WriteLine when they should position the screen cursor to the beginning of the next line. Like space characters and tab characters, newline characters are whitespace characters. The app of Fig. 3.11 outputs four lines of text, using newline characters to indicate when to begin each new line.

```csharp
1  // Fig. 3.11: Welcome3.cs
2  // Displaying multiple lines with a single statement.
3  using System;
4
5  class Welcome3
6  {
7    // Main method begins execution of C# app
8    static void Main()
9  {
```

Fig. 3.11 | Displaying multiple lines with a single statement. (Part 1 of 2.)
