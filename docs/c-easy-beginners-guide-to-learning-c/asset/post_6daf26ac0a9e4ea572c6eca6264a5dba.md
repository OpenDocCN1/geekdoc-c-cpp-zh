
![](img/a36030d08eb553093e54e93e07543b0a_28_0.png)

# Implicit Conversion

Data loss cannot occur when performing this conversion. Because it does not require an operator, it is referred to as implicit conversion. The C# compiler will perform an implicit conversion whenever you assign a narrow-range value to a variable with a wide range; the C# compiler will perform an implicit conversion.

# String Conversion

In C#, any type of data can be converted to a string. The compiler will automatically perform this conversion by using "+" and at least one non-string argument.

The non-string argument will be converted to a string with this operation, and the "+" operator will create a new value.

# Console

This chapter aims to teach you how to use the console to collect and provide data. Using this tool, you will learn to perform I/O (Input/Output) operations in C#.

# Console – The Basics

You can connect to your computer's console to interact with its programs. For this reason, consoles are viewed as a crucial part of any operating system.

Users and programs interact in C# using standard output (e.g., screen) and/or input (e.g., keyboard strokes). They are referred collectively as I/O operations. A computer program's text within the console provides useful data.

I/O devices on the computer are linked to every console program installed through your computer's OS (i.e., operating system). The default input and output devices on most computers are screens and keyboards. If you wish, you can easily redirect these channels to a particular file or device.

# Programming Interfaces and User Interactions

Users interact with most computer programs. Whenever a user interacts with a program, they must provide input and instructions. These days, there are many ways to interact: console-based, browser-based, internet-based, graphical, etc. As a result, the number of people using consoles to interact with programs is steadily decreasing. This is because the alternative options (e.g., browser-based) are more user-friendly and convenient.

# Using the Console

```
C:\Windows\system32\cmd.exe
Microsoft Windows Version [6.1.7601]
(C) 2009 Microsoft Corporation. All rights reserved.
C \Users\Sam>
```

Consoles can be very important for user interactions with programs.

When creating simple computer programs, you will need to use the console. For these programs, you will have to concentrate on the problems you need to fix. It will take more than attractive GUIs (i.e., graphical user interfaces) to succeed in this endeavor.

The console can also test a small code block before adding it to a complex program. It is very easy to isolate code blocks using the console since it is a simple tool. You will not have to use any buttons. In a few seconds, the console will provide you with the results that you need.

# How to access the console

Depending on the operating system you are using, you will have different ways to access the console. Here is what you need to do if you are using a Windows computer:

- 1. Press the Start button.
- 2. Click "Programs" and select "Accessories".
- 3. Click the "Command Prompt" option.

Your home directory will appear in the console, which is represented by your username. Let us look at an example: SARAH

You can run the console by searching for "cmd" in Windows Vista, Windows 7, or Windows 8.

# Here are some additional details regarding the console

Consoles display text-based information in a black window. The cursor blinks, and characters appear in a string. Whenever you type a character, the cursor moves.

Windows programs can run on desktops, browsers, Internet browsers, or consoles. These programs utilize consoles for input and output.

For user-program interactions, desktop-based programs rely on their GUIs. Throughout this book, you will be entering data using your keyboard, and you will see the results in the command prompt.

While working with a console-based program, you will use your keyboard a lot because some applications require text, numbers, characters, etc.

# Basic Commands

We will discuss the basic commands you will issue from the command prompt in this section. If you are interested in becoming a great C# programmer, you should study this material carefully.

# Using the console commands

You can change the active directory by using the command cd name.

- cd name: You can change the active directory by using the command cd name.
- dir: This command shows the contents of the directory.
- rmdir: This command deletes a directory.
- mkdir: This command allows you to create a new directory.
- type: This command displays the contents of a file.

# Standard I/O

For example, the C# language uses "Console.In" to control its input stream, "Console.Out" to send information, and "Console.Error" to report situations.

# Input and Output

Computers have a console for entering information. For example, the C# language uses "Console.In" to control its input stream.

# I/O Devices

Some programs accept keyboard input, barcode readers, microphones, and other data sources. Programs can also send their output to a screen, hard drive, or printer.

# System.Console

Text-based information can be read, displayed, or formatted using System.Console. Console.In, Console.Out, Console.Error are these attributes.

Data entry, information reading, and error reporting are made possible by these attributes.

# Console Input

Using Console.In directly is not necessary. There are two methods in the Console class (i.e., Console.ReadLine and Console.Read) that work with Console.In.

# Console.ReadLine Method

Simple and convenient, this method makes reading data from a console easy. Your program stops and waits for the user's input when you call this method. An individual can then enter a character or string and press "Enter". When the Enter key is pressed, the user tells the program that the necessary input has been entered using the console.ReadLine method, you can read the user's input.

You can see how console.ReadLine works by looking at the code given below:

```csharp
class Test
{
    static void Main()
    {
        System.Console.WriteLine("What is your first name?"); string yourfirstName = System.Console.ReadLine();
        System.Console.WriteLine("Please enter your last name?"); string yourLastName = System.Console.ReadLine();
        System.Console.WriteLine("Hi, {0} {1}!", firstName, lastName);
    }
}
```

The following message will appear if you enter "John" and "Smith" into the command prompt:
