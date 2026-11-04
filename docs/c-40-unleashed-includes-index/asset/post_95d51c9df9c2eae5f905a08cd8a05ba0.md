
![](img/a16f85e62ce9bdc527f4b09dbfe26092_196_0.png)

FIGURE 3.64 Test results.

Turns out I introduced some error in the Subtract method code, as caught by the unit test. Or the test could be wrong. Regardless, a failed test case screams for immediate attention to track down the problem. Notice you can also debug through test cases, just like regular program code.

Tightly integrated with unit testing is the ability to analyze code coverage. It's always a worthy goal to keep code coverage numbers high (90% as a bare minimum is a good goal, preferably more) so that you can be confident about the thoroughness of your test cases. Visual Studio actually has built-in code highlighting to contrast the pieces of code that were hit during testing from those that weren't.

## Team Development

To finish off our in-depth exploration of Visual Studio 2010 tooling support, we take a brief look at support for developing software in a team context. Today's enterprise applications are rarely ever written by a single developer or even by a handful of developers. For example, the .NET Framework itself has hundreds of developers and testers working on it on a day-to-day basis.

### Team System and Team Foundation Server

To deal with the complexities of such an organization, Visual Studio Team System (VSTS) provides development teams with a rich set of tools. Besides work item and bug tracking, project status reporting, and centralized document libraries, source control is likely the most visible aspect of team development.

The entry point for the use of Team Foundation Server (TFS) is the Team Explorer window integrated in Visual Studio 2010 (see Figure 3.65).

Here is a quick overview of the different nodes in the Team Explorer tree view:

- The root node represents the TFS server we’re connected to. One of the nice things about TFS is its use of HTTP(S) web services (so there is no hassle with port configurations). Underneath the server, different team projects are displayed.
- Work Items is the collective name for bug descriptions and tasks assigned to members of the team. Queries can be defined to search on different fields in the database. Via the Work Items view, bugs can be opened, resolved, and so on.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_197_0.png)

FIGURE 3.65 Team Explorer in Visual Studio 2010.

- **Documents** displays all sorts of documentation—Word documents, Visio diagrams, plain old text files, and such—that accompany the project. Those are also available through a SharePoint web interface.
- **Reports** leverages the SQL Server Reporting Services technology to display information about various aspects of the project to monitor its state. Examples include bug counts, code statistics, and so on.
- **Builds** allows developers to set up build definitions that can be used for product builds, either locally or remotely. It’s a good practice for team development to have a healthy product build at all times. Automated build facilities allow configuration of daily builds and such.
- **Source Control** is where source code is managed through various operations to streamline the process of multiple developers working on the code simultaneously. This is further integrated with Solution Explorer.

### Source Control

Source control stores source code centrally on a server and provides services to manage simultaneous updates by developers. When a code file requires modification, it’s checked out to allow for local editing. After making (and testing) the changes, the opposite operation of checking in is used to send updates to the source database. If a conflict edit is detected, tools assist in resolving that conflict by merging changes.

Figure 3.66 shows the presence of source control in Visual Studio 2010, including rich context menus in Solution Explorer and the Source Control Explorer window.

Other capabilities of source control include rich source code versioning (enabling going back in time), shelving edits for code review by peer developers, correlation of check-ins to resolved bugs, and the creation of branches in the source tree to give different feature crews their own playgrounds.

## CHAPTER 4

## Language Essentials

Essentials are important. This is no different with programming languages, so we start by focusing on the essences of the C# programming language: built-in types, variables, expressions and statements, control flow, methods, and so on.

### The Entry Point

To keep things simple, we’ll make exclusive use of console applications in the language-oriented chapters. Doing so allows us to concentrate on the essentials of the programming language without getting distracted by user interface definitions and so on.

One thing to consider first is the managed code entry point, which is where execution of the program starts. Different types of applications have such an entry point, including console applications and GUI applications built with Windows Forms or Windows Presentation Foundation (WPF). Other technologies, such as ASP.NET web applications, start execution of managed code in a different way, but let’s not go there now.

### A Trivial Console Application

By far the simplest managed code application that can be written in C# is one that doesn’t do anything useful. The following is only of academic interest, yet, but we have to start somewhere:

### IN THIS CHAPTER

- The Entry Point 171
- Keywords 177
- A Primer on Types 180
- Built-In Types 185
- Local Variables 209
- Intermezzo on Comments 220
- Arrays 228
- The Null Reference 237
- Nullable Value Types 240

```
class Program
{
    static void Main()
    {
    }
}
```

Main is the managed code entry-point method for our application. Its body, delimited by curly braces, contains the statements that get executed by the application. In this case, our method body is empty.

### CASE SENSITIVITY

Notice the casing of the Main method, with its first character uppercase. C# is a case-sensitive language, just like other C derivatives such as C++ and Java. In other words, method names that differ only in case denote different methods; so main and Main are not the same. C# requires the managed code entry point to be styled exactly as shown in the previous fragment.

Case sensitivity applies not only to method names. Keywords, names for types and their members, namespaces—they all are subject to case-sensitive treatment.

Let’s point out an important point immediately. For an assembly to be Common Language Specification (CLS)-compliant, no publicly visible type or member should differ only in case as compared to one of its peers. If this were the situation, non-case-sensitive languages like Visual Basic would be in trouble, resolving the name unambiguously.

C# doesn’t have the notion of global methods, meaning that all methods (and other sorts of members, as you will see) need to be contained in a type definition. In our example, the type is a class called Program. In the next chapter, we look at the distinction between types and classes, so ignore this detail for now.

### Method Signatures

Methods also have a signature, which you could see as the recipe that describes how the method is to be called. The important parts of a method signature include the method name, the return type, and the parameters. It also contains modifiers that are used to “modify” the behavior of the method.

Let’s decipher our Main method signature shown in Figure 4.1 with regard to these concepts:

- One modifier, the static keyword, is applied to the method. This means the method does not operate on a specific instance of the containing type. To explain this further, we first have to learn about types and object-oriented programming, which is subject of Chapter 14, “Object-Oriented Programming.” Stay tuned.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_202_0.png)

FIGURE 4.1 Decomposing the Main method signature.

- The return type of the method is void. As the name implies, this means the method returns nothing, making it a procedure. If the method were to return something, we would call it a *function*. Languages such as Visual Basic make this difference explicit by declaring procedures with a Sub keyword and functions with a Function keyword. C# doesn’t make this distinction: void indicates a procedure.
- As we already know, Main is the name of the method. This name is used to call the method (for example, from other places in the program or from other libraries). Main is a bit different, being the entry point called by the CLR directly.
- Our entry point has an empty parameter list surrounded by parentheses, meaning the caller can’t supply input for it when making a call. You’ll see in just a minute that different signatures for the entry point are accepted to deal with command-line arguments. Even when empty, this pair of parentheses cannot be omitted.

We refine the definition of a method signature in Chapter 10, “Methods,” when talking about visibility and generic methods.

### IS VOID A FIRST-CLASS TYPE?

Although we haven’t learned about types just yet, the curious reader will no doubt wonder whether void, something used to denote nothing, is a true type. Slightly disappointing, the answer is no. You’ll see later why such a first-class treatment could be useful, but to be honest it’s not a big deal.

### Allowed Entry-Point Signatures

As we all know, invocation of programs in operating systems supports passing in command-line parameters. In addition, executables can provide an exit code upon termination, indicating the result of the invocation, with a zero value typically denoting a success state. To enable those scenarios, four different signatures for the Main method are permitted:

```
static void Main()
static int Main()
static void Main(string[] args)
static int Main(string[] args)
```
