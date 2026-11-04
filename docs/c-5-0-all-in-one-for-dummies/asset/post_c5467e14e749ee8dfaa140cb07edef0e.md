
![](img/80ff26f06fc9ab951e1cd4257b867366_552_0.png)

Figure 2-7: Paneling your property.

When I say it shows endless lists of details about everything, I mean everything. If you click nearly anything in Visual Studio and press F4 to bring up the Property Panel (refer to Figure 2-7), you will get properties. Try it with these fun selections:

- Files in Solution Explorer
- Database connections
- A textbox in a WPF project
- An XML tree node
- An item in Class View

If there is any meta-data about something, the properties are in the Property Panel. It's a great tool.

## The Toolbox

One of the great misunderstood tools is the Toolbox (see Figure 2-8). On the surface, the Toolbox seems so simple. The design-time controls for a given file type are available to drag and drop. Still, there is one important thing you need to remember about the Toolbox. Wait, I'll get out my Remember icon.

![](img/80ff26f06fc9ab951e1cd4257b867366_553_0.png)

The Toolbox displays only controls that are appropriate to the file in focus.

So, if you’re running a Windows Form in the designer, you won’t see a database table available to drop. Trust me; if you expect to see a certain control, and it isn’t there, the Toolbox probably isn’t messed up. If there isn’t a file open, the Toolbox is empty. That’s by design.

![](img/80ff26f06fc9ab951e1cd4257b867366_553_1.png)

**Figure 2-8:**  
The Toolbox, with tools.

I can’t tell you how many times I have been expecting to see something in the Toolbox only to find it blank. Then I spend ten minutes tracking down the problem, only to realize that the problem is mine — I didn’t have a file open. I once actually called Microsoft because I couldn’t find a maskedtextbox for my Web Forms project.

There is no maskedtextbox for Web Forms projects.

So keep it in mind that the Toolbox is context-sensitive. It works only when it has a file to work on.

There is one other interesting property of the Toolbox: It can be used to store text clippings, which can be useful for demonstrations and presentations. It is also handy for storing often-used pieces of code (Book I Chapter 1), but snippets (covered in Chapter 3) are even better. To do so, follow these steps:

- 1. **Open a code file.**

   Anything will do, `.cs` file, `.xaml` file, whatever.

- 2. Highlight a piece of code.

- 3. Make sure the Toolbox is open and then drag the selected code to the General section of the Toolbox.

   The copied code becomes a tool.

- 4. Open up another blank code file.

- 5. Drag the new tool into the code.

   The copied code now appears in the code file.

## Server Explorer

Server Explorer (see Figure 2-9) isn't in every version of Visual Studio. At the time this book was printed, it was included only in the Professional Edition and higher.

![](img/80ff26f06fc9ab951e1cd4257b867366_554_0.png)

Figure 2-9: Server Explorer.

Server Explorer enables developers to access important services on a remote machine. These could be anything from SharePoint to Microsoft Message Queue (MSMQ) but generally include two types of services:

- Managed services
- Database connections

### Managed services

Managed services are things like Event Viewer and MSMQ: things that you would need to look at to test parts of your application. Internet Information Services, for example, is a managed service that would show up in the list.

To get a server into Server Explorer, follow these steps:

- 1. Right-click Servers.
- 2. Click the Add Server button.
- 3. Type the machine name or IP number of the server you want to add.
- 4. If you want to use different credentials than you used to log in (for a different account, for instance), click Connect Using a Different User Name and enter the new credentials.
- 5. Click OK.

Play around with the services you see. There are a lot of features in this panel that I don't have space to get into here.

### Data connections

Above the Services in Figure 2-9 are the data connections. These are data connections that have been made on previous projects, which Visual Studio keeps around in case you need them for any other projects. Although keeping these connections around seems like a bit of a security risk, it sure as heck is convenient.

The goal is to reduce the dependency on SQL Management Console (the old method for managing the database for developers), and it does a darn good job. The key issue is access to the data model (table names and columns) and stored procedures; developing a program without access to the database is tough.

In a new connection, these database objects are given default folders:

- Database diagrams
- Tables
- Views
- Stored Procedures
- Functions
- Types
- Synonyms
- Assemblies

The key thing I want you to try is opening a Stored Procedure (you can do this by double-clicking it in the Data Sources panel — which is available in a solution that has data connections). When you do so, you can easily edit SQL code, with indenting and colorization, right in Visual Studio. Use this. It's really neat.

## Class View

The last of the five main panels is Class View. As I discuss throughout Books I and II, everything in the .NET Framework is an object. The classes that make up the framework — all derivatives of Object — are viewable in a tree view.

The Class Viewer is the home for that tree view (see Figure 2-10).

![](img/80ff26f06fc9ab951e1cd4257b867366_556_0.png)

Figure 2-10: A viewer with Class.

From the Class View, you can look at all the members of a class and access the inline documentation, which gives you an overview of the framework and custom classes that make up your project.

## Coding in the Code Editor

Really, what else would you do in the Code Editor? Nothing, that's what!

There is a lot to the Code Editor in Visual Studio. Fact is, this is where you will spend 75 percent of your time, and boy, will you be glad that it works well.

Code Editor has two primary tools:

- **The Editor itself:** The first is the screen on which you edit the code — the Code Editor.
- **Auxiliary windows:** The second are the little auxiliary windows that do a lot of useful things that don't directly relate to the code.

### Exercising the Code Editor

The Code Editor is where you edit code. Doesn't matter what type of code, all of it is edited here (see Figure 2-11).

![](img/80ff26f06fc9ab951e1cd4257b867366_557_0.png)

**Figure 2-11:** Viewing the Code Editor.

It is a smart tool, however. If you are in XML, it works like an XML editor. In C++, it helps with the tabbing.

You can get to a code file in the Code Editor a few ways. The most common way is to double-click on a source code file in Solution Explorer, and it will open in Code Editor.

If you are viewing something in the designer, you can get to the code-behind related to the file in question by any of three methods:

- Click the View Code button in Solution Explorer.
- Right-click the design surface and select View Code.
- Double-click a control in the designer to generate an event for that control and be moved to Code View.

You'll find yourself using all three over time. Note that you can get directly to the code-behind files by clicking the little triangle next to a designer file and then double-clicking the code files nested within.

### Autocompleting with IntelliSense

IntelliSense is Microsoft's autocompletion feature, and it's a prominent part of the Code Editor. You find IntelliSense whether you want to or not. In Code View, click inside a class and press Ctrl+spacebar. Everything you are allowed to type there shows up in a big list.

The nice thing is, IntelliSense is context-sensitive. Type `Console` and press the dot (`.`). All available members of Console appear. IntelliSense keeps you honest and prevents having to remember the two-million-odd members of the .NET Framework on a day-by-day basis.

IntelliSense helps with method signatures, too. Continue the line you started earlier by adding `WriteLine` — in other words, type `Console.WriteLine(` — then check out the IntelliSense. It will tell you all the overloads for the member in question. Use the up and down arrows to move between them. It's slick.

### Outlining

Visual Studio will auto-outline your code for you. Notice the little box with a minus sign (–) next to every namespace, class, and method in the code editor (see Figure 2-12)? Those are close-up sections of the code for readability. Doesn't seem like much now, but when you have 2,200 lines of code in there, you will be glad.

You can create your own outlining, too. Preceding a section that you want to outline, put `#region` on a new line. After that section, put `#endregion`. This newly defined section — regardless of whether it's at an existing outline point — will get a new outline mark.

If there is a comment added after a `region` statement, it will show in the collapsed outline — as you can see in Figure 2-12.
