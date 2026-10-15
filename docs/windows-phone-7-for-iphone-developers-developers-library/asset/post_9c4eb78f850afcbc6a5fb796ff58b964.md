
![](img/04a00d46bb1059867d95707babd62ee7_79_0.png)

Figure 6.7 Docking target shortcut icons.

## Summary

A developer’s IDE is like a mechanic’s toolbox. It isn’t just a single wrench or a single screwdriver. It’s everything needed to build applications. As a result, developers spend the vast majority of their development time sitting in front of that IDE.

Because of that, IDE creators spend an awful lot of time trying to make sure that their tools are fast, efficient, and—most important—easy to use. Visual Studio and Xcode are two of the most powerful IDEs available for building mobile applications today. In many ways they are similar, but there are also a lot of fundamental differences. The thing that I hope you take away from this chapter is that both of them are so configurable and so flexible that you should be able to make them lay out your environment in such a way that is comfortable to you, no matter how you like things set up.

Visual Studio will become your best friend as you progress throughout this book. You will use it for writing your XAML, for writing your C#, for debugging, for profiling, for running your application, for building your application, and even for getting it ready to be deployed to the marketplace. Taking the time now to step back from the code and familiarize yourself with this tool will go a long way toward making the rest of the book easier to plow through.

This page intentionally left blank

## Introducing Expression Blend

> I think design covers so much more than the aesthetic. Design is fundamentally more. Design is usability. It is Information Architecture. It is accessibility. This is all design.
> 
> Mark Boulton

This chapter provides you with an introduction to Microsoft’s interaction design tool, Expression Blend. I start with an overview of Interface Builder, the application iOS developers often use to build their user interfaces. Next, I provide a walkthrough of Expression Blend—its purpose and key features and how it differs in form and function from that of Interface Builder.

In the previous chapter we walked through Visual Studio and its features that enable you to write code and compile and run applications. This chapter is all about design tools, how to use them, and more importantly, when you should use them.

### Overview of Apple’s Interface Builder

Interface Builder (IB) has been around for quite some time, and Mac developers have been using it to construct view hierarchies for desktop Cocoa applications for years. With the release of the original iPhone SDK, Interface Builder was tasked with giving developers a way to manipulate user interfaces in a near-WYSIWYG fashion.

Before diving into a description of how IB works, I think it’s worth including a paragraph with a brief history lesson. Many people assume that the first release of the iPhone also came with the first release of the SDK. This isn’t actually how it happened. When the iPhone 1.0 was first released, the “SDK” was Safari. There was no App Store, no Marketplace, and no Objective-C SDK. All developers could do was build web applications that used clever JavaScript, HTML, and CSS trickery to make those web applications look and feel like iPhone applications. To this day, many websites still have “iPhone-y” UIs that are presented when an iOS device browses to that site. One year later, the iPhone SDK was released. This SDK included Xcode and the capability to run applications on a simulator and upload applications to the App Store. However, this SDK did not include Interface Builder. Or rather, Interface Builder could not be used in conjunction with iPhone SDK projects. It wasn’t until months later that a revision to the iPhone SDK included Interface Builder support. We should all count our blessings that Microsoft released not one but two designers with its v1 product: Expression Blend and the VS2010-embedded designer, which share quite a bit of code.

Interface Builder is just as its name implies: a tool for building interfaces. As you can see in Figure 7.1, it does a fairly good job of giving you an estimate of the user interface that will be rendered when the application runs. Also keep in mind that older versions of Xcode and Interface Builder were separate tools, whereas with versions 4 and later, Xcode and the “visual designer formerly known as Interface Builder” are one and the same.

![](img/04a00d46bb1059867d95707babd62ee7_82_0.png)

Figure 7.1 Building a UI with the Xcode 4 Designer.

The rub, of course, is that the UI that IB shows you at design time is just a rough estimate. For example, when you’re working with a TableViewController and you are trying to set up a UI that will display a list of items using a custom cell, there’s no way for IB to give you all of that merged into a single design surface. Take a look at Figure 7.2, which shows how a typical developer might use IB to rig up a TableViewController with a custom table view cell. You can’t see what the cell is going to look like within the table; you can only look at one sell separately in a different window while IB provides a “simulated” UI for the table itself. As you’ll see later in this book in Chapter 16, “Separating Your Concerns,” not only can you see custom list boxes at design time in WP7 and Visual Studio, but you can even provide sample data to which you can bind your controls at design time to get a really good preview of the final rendering.

![](img/04a00d46bb1059867d95707babd62ee7_83_0.png)

Figure 7.2 Working with a TableViewController in Xcode/Interface Builder.

At its core, Interface Builder is taking a configuration of an object hierarchy (such as a view hierarchy including view controllers and subviews) and storing that information in a special file called a “nib” (although the more modern equivalent of this file is an XML file with the XIB extension, still called “nib” because it’s much easier to pronounce).

By setting your main window’s configuration through Interface Builder, you are indicating the state you would like that window to be in after the application has started up. When a reference for your main window is asked for by the application, it will take all the information contained in the XIB file and use it to create a fresh instance of a window object. This pattern continues throughout your application as UI objects are needed, including custom table view cells like the one shown in Figure 7.2.

This differs from the way designers work with Silverlight applications in that Interface Builder really just creates data files. These data files are written by Interface Builder and read by the application at runtime to generate instances of objects. Silverlight applications use XAML as a markup language to describe the instantiations that should occur. This is a subtle but important difference. XAML is an instantiation language. It uses XML to describe the objects that should be instantiated and the properties within those objects that should be set.

This is a subtle but important difference because there are some things that require a live, running application to render in iOS, which is why Interface Builder often supplies only “simulation” UI-like fake navigation bars, tab bars, and the like. The point at which iOS developers need to write pure Objective-C and where they need to build their UI in Interface Builder is often confusing, and the consequences for getting this split wrong can be immense. Some seasoned iPhone developers rarely use IB, and often use it only when there is no other alternative. Other iPhone developers have an IB-first approach in which they build everything in Interface Builder until they absolutely cannot get away without writing custom code in Objective-C. As you’ll see later in Chapter 16 on MVVM (Model,View,ViewModel—a pattern for separating concerns when building user interfaces), because everything can be represented as XAML (even the objects to which your UI is bound), you can get an almost exact replica of your final UI inside either Expression Blend or Visual Studio without the need for mocked elements.

XAML is considered a first-class citizen in the Microsoft development environment. iOS developers never look at the serialization format used by IB; they either work in Objective-C or the point-and-click UI of the designer. Microsoft developers work in XAML all the time and, as you’ll see in the screenshots in this book, many developers often type the XAML and watch the immediate effects of the markup on their UI.

### Introduction to Expression Blend

When I first heard that Microsoft was working on an XAML design tool that would help developers build amazing UIs, guide them through building complex animations, and much more, I was a little skeptical. In fact, my reaction was something along the lines of, “Microsoft? Build a design tool? Inconceivable!”

However, over the years I’ve learned that first impressions (especially those clouded by prejudgment and simple ignorance, rather than those formed by an actual impression) are often wrong. I decided to give Expression Blend a try. As a somewhat relevant aside, I am not a designer. I have no digital design skills and prefer the comfort and form of a pencil to that of a mouse. I’ve never gotten along well with Photoshop, and I’ve always written my HTML in Notepad (or other text editors). I have also almost exclusively written my XAML in Visual Studio’s text editor with the design surface actually removed, seeing the finished product only after running the application. I have been what you might consider the exact opposite of the target user for a design tool such as Blend. I fought it and resisted it like the plague. I was going to curmudgeonly refuse to adopt this shiny new tool no matter the cost. That was before I tried it.

At its core, all Blend does is provide you with a robust UI sitting on top of an XAML editor. All the fancy things you do with all the controls, widgets, knobs, trays, and panels eventually boil down to the manipulation of XAML (and occasionally C#) in your project. The interesting part is that, unlike my past experience with design tools that produce markup (yeah, I’m looking at you, FrontPage), Blend actually reduces the amount of time it takes you to build a UI, and—here’s the shocking part—it actually produces clean XAML. If you want to take a few minutes and sift through some online tutorials to get you familiar with Expression Blend, I recommend you check out this URL: http://expression.microsoft.com/en-us/cc184874.aspx. If you want a full reference on building Silverlight 4 applications with Expression Blend (the vast majority of which will still apply to WP7 development), check out Expression Blend 4 with Silverlight, by Victor Gaudioso.
