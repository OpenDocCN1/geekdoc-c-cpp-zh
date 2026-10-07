
2. Inside that .cs file, you should write the source code.
3. Make a .exe file by compiling the code.
4. Run the program you created.

Let us start by turning on your computer.
It would be best if you use a Windows computer in order to use this eBook.
The HelloCSharp program code is as follows:

# Command Prompt for Writing C# Programs

As a first step, you should launch the "Command Prompt" (also called the "Command Console").
You can run a search for "cmd" using the Start button to use Windows 7 or Windows 8. Find the program named "Command Prompt" in the search results. To run the program as an administrator, right-click the program and select "Run as administrator".

The following screenshots show how it looks:

![](img/a36030d08eb553093e54e93e07543b0a_8_0.png)

Please take note that if you double-click on the Command Prompt, you will not be able to access "C# access some of its essential features."

Create a directory to store the resulting program after you create the file.
After you select the directory, type "md". Press "cd" to go to the new directory.

The following screenshot shows how it looks:

![](img/a36030d08eb553093e54e93e07543b0a_9_0.png)

It is named "C#Programs" in this example.
C:/Windows/System32/C#Programs became the active directory by using "cd". The C# file is now ready to be created. You will see this on your screen after you run this command in the Command Prompt. CSharp does not exist on your computer. Additionally, it will ask if you want to create a new file. To copy the program's code, click on the "Yes" button and paste it into Notepad.

The following screenshot shows how it looks:

![](img/a36030d08eb553093e54e93e07543b0a_9_1.png)

Save the file by pressing CTRL+S. Press ALT+F4 or the red X to close the text editor. It appears under the "C#Programs" directory now.

Composing the code

Once the code is compiled, you can run it using "csc" (the language's built-in compiler). Open the Command Prompt and enter "csc HelloCSharp.cs". You might receive a message similar to this, as this is the first time you have used the C# compiler: To overcome this issue, specify the location of the C# compiler. For Windows 7, the location is as follows:

C:\Windows\Microsoft.NET\Framework\v4.0.30319

Note: You may see different numbers at the end of the directory depending on your OS version.

Therefore, the following command should be issued:

Here is the C# source for HelloCSharp.cs:
```csharp

```cs
C:/Windows/Microsoft.NET/Framework/v4.0.30319/csc The C# compiler will convert your .cs file into an executable. In the Command Prompt, type the name of your first program.

# Windows System Path Change

When you create a program, surely you do not want to type the entire directory path for the compiler. Throughout this chapter, you will be taught how to configure your computer to find the compiler automatically.
The following things need to be done:

- 1. In the Control Panel, select "System".
2. A new window will appear. Click on "Advanced System Settings".
3. You can find the variable "Path" by clicking on "Environment Variables".
4. Then select the directory for the compiler by clicking the "Edit..." button. Here is the path again:
C:\Windows\Microsoft.NET\Framework\v4.0.30319
5. Save the changes by clicking "OK".
6. Launch a new Command Prompt after closing the current one. Enter the command "csc".
7. This error message should appear on your screen:

```
Fatal error CS2008: No inputs specified
```

- 8. This means that your computer can automatically initiate the compiler. Your computer will create .exe files from the source code when you specify it.

# Variables, Literals, and Data Types of C#

The purpose of this chapter is to cover the variables and data types used in C#. After reading this material, you will learn what these objects are and how to write your programs.

## Variables

Different values are used during the execution of specific programs. Mathematical problems can be solved with a program. When you use such a program, you must enter different values. Programmers do not know what values users will enter. Therefore, they should make sure that any input that users provide is included in the resulting programs.

It is possible to temporarily store a user's value in the machine's RAM (i.e., random access memory). These values may change over time. Programmers call such values "variables" because of this.

## Data Types

A data type consists of a group of values whose attributes are similar. As an example, among the "0 to 255" range of values, these are referred to as "byte" data. These are the attributes of data types:

- The name of the type of data (i.e., int, char, bool, etc.).

## C# Data Types

- Boolean
- Characters
- Objects
- Floating Points
- Decimals
- Integers
- Strings
