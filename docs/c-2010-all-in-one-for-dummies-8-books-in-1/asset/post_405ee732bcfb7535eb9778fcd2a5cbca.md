
# 496 Designing in the Designer

For each major type of project that Visual Studio maintains, there is a designer. The designer handles the What You See Is What You Get portion of the experience and usually the behind-the-scenes markup code.

The problem is that because of the necessities of the software development world we live in, designers all work a little differently. A significant difference exists between HTML and XAML, for example, the Web designer and the WPF designer don't look or act the same.

Visual Studio gives you several visual designers to help develop applications, including these:

- Class Designer
- Data View
- Windows Forms
- Windows Presentation Foundation

## Windows Presentation Foundation (WPF)

Windows Presentation Foundation is covered in some depth in Book V, but for now you should know that it is the future of Microsoft's Windows development experience. Book V talks all about WPF, so you can read more about it.

The core of the user interface design is a language called XAML, which (surprisingly) is an XML-derived domain-specific markup language for the creation of user interfaces. In the Designer, shown in Figure 2-1, the design is in the top frame, and the underlying code is in the bottom frame.

You can click the design in the designer and move things around, if you want, or use the designer to select things and edit the properties in the Properties panel (which I cover in the upcoming section “Paneling the Studio”). Additionally, if you change something in the code area, you will see the change in the design. It's a good system.

There are a few but significant features in the WPF designer that should be pointed out. You can see all them in Figure 2-1.

Near the upper-left corner is a zoom bar. You can click the bottom of it and Zoom To Fit, or move the slider. This is invaluable for working on an application that is bigger than your screen, or lightening things just so.

At the left side of the dividing line between the Design and XAML frames are a little double-arrow icon. Clicking this icon changes whatever is in the bottom frame to be in the top frame, and vice versa.

# # Designing in the Designer 497

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_522_0.png)

**Figure 2-1: The WPF Designer.**

On the right side of the same dividing line there are three buttons that determine the kind of split you have — a vertical split, a horizontal split (which is default), or no split.

A few point-and-click adjustment tools are in the designer itself. Here's just one: Click in the red area of the table in the window of the designer. Put your mouse right above where the "146" size designation appears.

See the little box that appears, with an asterisk, a hash, and the word *Auto*? That's one of the many helpers you find in the WPF designer. The hash sets the column width to a number (as it is by default). The asterisk sets it to a percentage of the table — useful for resizing. The word *Auto* sizes the column based on the contents.

These little features make changes only to the XAML in the frame below the designer. If you click the word *Auto* in the floating table designer, you will change this line of code:

```
<ColumnDefinition Width="146" />
```

to this line of code in the XAML frame:

```
<ColumnDefinition Width="Auto" />
```

# 498 Designing in the Designer

Some people like the code. Some people like the designer. Some people (like) prefer a strange mixture of the two. You determine how you want to use the tools.

## Windows Forms

The main difference between the Windows Forms designer and the WPF designer is the lack of a code panel in Windows Forms. Although there is code (of sorts) backing up Windows Forms, you don't get to edit it. So there.

The topic of Windows Forms isn't covered in this book. Though it's still an active development platform, I had to make the tough call to cover WPF instead. It performs the same programming duties as Windows Forms but is the newer technology. The Windows Forms designer is shown in Figure 2-2.

In truth, there is little to say about the Windows Forms designer itself. The individual controls have some nice designer features, but the designer itself doesn't much.

It should be said, though, that I don't do much with Windows Forms in this book. First, this isn't a Windows programming book; it is a C# book. Second, Windows Forms is on its way out. WPF is the future of Windows programming. Windows Forms is just for backward compatibility.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_523_0.png)

Figure 2-2: The Windows Forms designer.

# Designing in the Designer 499

## Web Forms

Web programming resembles WPF programming than it resembles Windows Forms programming, but it's run from a Web server and viewed in a browser. (Book VI is all Web Forms.) Because the designer has a back-end code element, you can see a split view, as shown in Figure 2-3.

Getting around in the HTML designer is easy. I want to point out two features in particular about the HTML designer. These features can be found in a menu strip along the bottom of the designer:

- The view change buttons, which read Source, Design, and Split: Source shows only the HTML code. Design shows only the visual designer. Split, surprisingly, both in two panels, just like the WPF designer.

- Interestingly, the two frames do not stay in sync. If you change the HTML, the design frame shows a message that "Design is out of sync with Source view. Click here to synchronize views. Here's hoping they fix that before they release to manufacturing.

- The small document tree to view the view change buttons: This shows in the hierarchical tree where your cursor is its relationship to the rest of the document.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_524_0.png)
![](img/36596fb11aa4233d5cab0d6ddd1d82e8_524_1.png)

Book IV Chapter 2
Using the Interface

Figure 2-3 Back to code with Web projects.

## Class Designer

You can make a Class Designer from any project, but I used a Class Library project for my next example, shown in Figure 2-4:

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_525_0.png)

Figure 2-4: My garden, in digital form.

The class designer gives you a visual interface into a class library. You can easily see the inheritance, and the members are visible and editable. Here is the class library I used for Figure 2-4:

```
namespace MyGarden
{
    public class Flower
    {
        public string Color;
    }
    public class Vegetable
    {
        public bool Yummy;
    }
    public class Daisy : Flower
    {
        public double Height;
    }
    public class Sunflower : Flower
    {
        public bool Harvested;
    }
    public class Tomato : Vegetable
    {
    }
    public double StakeHeight;
}
public class Carrot : Vegetable
{
    public double Depth;
}
}
```

To create a class library like this, follow these steps:

1. Create a new Class Library project.
2. Replace the default code with a listing of your own.
3. Build the class library by pressing Ctrl + Shift + B.
4. Right-click on the project and select Class Diagram.
   You can use the one in this section, if you want.
   Visual Studio creates a new file called ClassDiagram.cd. This is your Class Diagram file.
5. Save your project.

You can add to your new class as well. Click on the Methods of the Flower class and add a Water method by typing Water under name under type, and Public under modifier. If you change back to the library view, you'll find there a method has been added to the code under that class.

> To aid in documentation of projects, you can right-click anywhere in the designer pane and select Export This Diagram as an Image, and save it off as a PNG file. I find this immensely useful when I am creating documentation for a project. It is a lot more useful than Visio because it is integrated with your code, included in Visual Studio, and it's free!

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_526_0.png)

# Data View

Data View is usually used with the Server Explorer and is part of an in-data representation of SQL Management Studio. You can view and edit data tables in the SQL Server (and other) database management system right inside Visual Studio. An example is shown in 2-5.

There is a remarkable amount of power here, and there just isn't enough space to cover it all. Again, this isn't a database book, so I recommend reading over the MSD entries for the Data Connections feature of SQL Explorer for more details.
