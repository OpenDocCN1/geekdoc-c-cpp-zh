# WindowForms and Web-based Application Development on .NET

# 20.1 Introduction

.NET is a software programming architecture provided by Microsoft for developing applications, which can be run on the Web through a network connection such as Internet or Intranet. The applications, which are developed for the Web using .NET are called Web based applications. .NET supports the ASP.NET technology with C# programming for allowing software developers to create Web based applications, which can be used to perform tasks such as validating data received by the server from client computers and doing business on the Internet. The Web-based application can be created for allowing users who are surfing the Internet to do online shopping. .NET also allows software developers to develop Windows based applications for performing tasks such as accessing data from a database and manipulating that data. We can use Microsoft Visual Studio 2005 to develop Web based and Windows based .NET applications.

Before we start using Visual Studio for developing applications, let’s get ourselves familiar with the basic building block of a Windows application—form.

# 20.2 CREATING WINDOWFORMS

Form is the very first entity typically included in a Windows-based application. It hosts a number of other controls for performing desired functions. At runtime, a form continuously waits for an event to occur, such as the clicking of the mouse or pressing of a key. As soon as an event occurs, it triggers the corresponding event-handling code.

In C#, a form can be created by inheriting the Form class contained in the System.Windows.Forms namespace. The Form class already supports a number of properties and methods, which make the job of the programmer a lot easier. Let us now create a simple blank form by making use of the Form class:

# Program 20.1 CREATING A SIMPLE BLANK FORM

```
//Program - SampleForm.cs
using System.Windows.Forms;
public class SampleForm : Form
{
```