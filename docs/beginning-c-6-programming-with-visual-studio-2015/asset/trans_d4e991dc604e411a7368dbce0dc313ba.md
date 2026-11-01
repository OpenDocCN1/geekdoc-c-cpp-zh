
The Dispatcher is used to invoke the call. This ensures that the calls are made on the GUI thread.

Drawing the cards is pretty straightforward. The program simply stacks them vertically or horizontally depending on the settings in PlayerOrientation.

The GameDecksControl is even simpler. It uses the CurrentPlayer class to be notified that the CurrentPlayer has changed. When this happens, it hooks the CardDiscarded event on the player, and uses this event to be notified that the card was discarded.

Finally, you add a dock panel to the game client with a CardsInHandControl on each side and with a GameDecksControl in the middle:

```
<local:CardsInHandControl x:Name="Player1Hand" DockPanel.Dock="Top"
HorizontalAlignment="Center" Height="154" VerticalAlignment="Top"
PlayerOrientation="Horizontal" Owner="{Binding Players[0]}" Width="380"
PlayerState="{Binding Players[0].State}" Game="{Binding}" />
```

The binding for Game simply binds the DataContext of the game client directly to the Game property of the CardsInHandControl. The PlayerState is bound to the State property of a player. In this case, the player at index 0 is used to access the state.

### EXERCISES

15.1 The current game client has a problem. From the Options dialog box, you can set the skill level of the computer. The problem is that the radio buttons are not updated to reflect the choice the next time you open the Options dialog box. This is partly because there is nothing that tries to update them and partly because there is no value converter from ComputerSkillLevel. Fix this problem by creating a new value converter and setting the IsChecked binding instead of using the Checked event that is currently being used.

Hint: You must use the ConverterParameter part of the Converter binding.

15.2 The computer cheats, so you might want to allow the players to cheat as well. On the Options dialog box, create an option for the computer to play with open cards.

15.3 Create a status bar at the bottom of the game client that displays the current state of the game.

### WHAT YOU LEARNED IN THIS CHAPTER

| TOPIC | KEY CONCEPTS |
| --- | --- |
| Styles | You can use styles to create styles for XAML elements that can be reused on many elements. Styles allow you to set the properties of an element. When you set the `Style` property of an element to point to a style you have defined, the properties of the element will use the values you specified in the `Style` property. |
| Templates | Templates are used to define the content of a control. Using templates you can change how standard controls are displayed. You can also build complex custom controls with them. |
| Value converters | Value converters are used to convert to and from two types. To create a value converter, you must implement the interface `IValueConverter` on a class. |
| User controls | User controls are used to create code and XAML that can be reused easily in your own project. This code and XAML can also be exported for use in other projects. |

## 16 Basic Cloud Programming

### WHAT YOU WILL LEARN IN THIS CHAPTER

- Understanding the cloud, cloud programming, and the cloud optimized stack
- Programming for the cloud using cloud design patterns
- Using Microsoft Azure C# libraries to create a storage container
- Creating an ASP.NET 4.6 Web site that uses the storage container

### WROX.COM CODE DOWNLOADS FOR THIS CHAPTER

The wrox.com code downloads for this chapter are found at www.wrox.com/go/beginning-visual-c-2015-programming on the Download Code tab. The code is in the Chapter 16 download and individually named according to the names throughout the chapter.

In this book, the basics of C# programming are conveyed mostly using console applications, desktop applications with WPF, and Windows Universal Apps. Although these are viable and compelling development techniques, they are not good examples of programs to host and run in the cloud. These kinds of programs are classically deployed to and run on a user's computer, tablet, or mobile device. These programs are compiled into executables or dynamic linked libraries that have dependencies on preinstalled software like the .NET Framework, for example. These dependencies are generally assumed to be present on the location where they are installed, or they get included in the installation procedure. By contrast, an Internet application that is run in the cloud, based on ASP.NET, for instance, cannot rely on any such library or dependency being present on the computer or device from which the program is accessed. All dependencies instead are installed on the server hosting the Internet application and are accessed by a device using protocols such as HTTP, WS (web socket), FTP, or SMTP. Although console, desktop, and Windows Universal Apps can have dependencies in the cloud, like databases, storage containers, or web services, they themselves are generally not hosted there.

Programs that are accessed via web browsers and respond to REST API or WCF service requests are good candidates for running in the cloud. Development techniques used for creating those program types do not require any built-in dependency on the device from which they are called. In typical cases, those program types merely exchange information between themselves and render data in a legible and user-friendly fashion. Additionally, programs that receive and process large amounts of data are good candidates for running in the cloud, as utilizing the hyper-scalability of resources to accept and process the data is a fundamental feature of the cloud itself.

This chapter provides an overview of what the cloud is, some examples of patterns and techniques for successfully running a program in the cloud, and an example of creating and using cloud resources from an ASP.NET web site.

### THE CLOUD, CLOUD COMPUTING, AND THE CLOUD OPTIMIZED STACK

It is only a matter of time before you begin creating applications that run completely or partially in the cloud. It's no longer a question of "it" but "when." Deciding which components of your program will run in the cloud, the cloud type, and the cloud service model requires some investigation, understanding, and planning. For starters, you need to be clear on what the cloud is. The cloud is simply a large amount of commoditized computer hardware running inside a datacenter that can run programs and store large amounts of data. The differentiator is elasticity, which is the ability to scale up (for example, increase CPU and memory) and/or out (for example, increase number of virtual server instances) dynamically, then scale back down with seemingly minimal to no effort. This is an enormous difference from the current IT operational landscape where differentiated computer resources often go partially or completely unused in one area of the company, while in other areas there is a serious lack of computer resources. The cloud resolves this issue by providing access to computer resources as you need them, and when you don't need them those resources are given to someone else. For individual developers, the cloud is a place to deploy your program and expose it to the world. If by chance the program becomes a popular one, you can scale to meet your resources needs; if the program is a flop, then you are not out much money or time spent on setting up dedicated computer hardware and infrastructure.

Let's explore cloud type and cloud service models in more detail now. The common cloud types are public, private, and hybrid and are described in the following bullet points and illustrated in Figure 16-1.

- Public cloud is shared computer hardware and infrastructure owned and operated by a cloud provider like Microsoft Azure, Amazon AWS, Rackspace, or IBM Cloud. This cloud type is ideal for small and medium businesses that need to manage fluctuations in customer and user demands.
- Private cloud is dedicated computer hardware and infrastructure that exists onsite or in an outsourced data center. This cloud type is ideal for larger companies or those that must deliver a higher level of data security or government compliance.
- Hybrid cloud is a combination of both public and private cloud types whereby you choose which segments of your IT solution run on the private cloud and which run on the public cloud. The ideal solution is to run your business-critical programs that require a greater
