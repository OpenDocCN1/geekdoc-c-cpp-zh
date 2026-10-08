and designers to work separately. Developers ensure that data gets to the client and back to the server, and designers can independently create the data visualization and entry mechanisms for Homo Sapiens 1.0.

The rest of this chapter gives a quick overview of Silverlight and WPF. Because the basic concepts are almost the same for both technologies, Silverlight will be examined first. The second part of the chapter discusses the differences between Silverlight and WPF, and provides guidelines for choosing between the two. You will finally return to the designer-developer cooperation and learn about how these tools can help this cooperation become a reality.

# A NEW GENERATION OF PRESENTATION FRAMEWORKS

In 2001, Microsoft founder Bill Gates created a new team tasked with researching and developing a new presentation layer. .NET 1.0 wasn't released at this point. At that time, there were at least four different, but overlapping, UI technologies within Microsoft: Windows Forms, GDI32, Visual Basic, and Internet Explorer’s Trident engine. The technology to be created by the new group was named "Avalon".

> You can learn more about the history and goals of Avalon in Chris Anderson’s book, Essential Windows Presentation Foundation (Reading, MA: Addison-Wesley, 2007).

The Avalon team aimed to merge the best of the web and the desktop, to integrate first-class multimedia with documents and UI, to streamline the designer-developer workflow, and to create a rich presentation platform that could easily increasing the power of graphics hardware.

The first appearance of Avalon was in 2003, at the Professional Developers Conference (PDC). Later, Avalon was renamed Windows Presentation Foundation (WPF), and it appeared in version 3.0 of the .NET Framework. WPF was still a novelty at the time. With limited and (buggy) support in Visual Studio 2005, and a nonexistent designer tool, many were reluctant to climb the steep learning curve. Still, the most important thing was already there: a solid, well-thought architecture and foundation that could be built upon. The pillars of WPF are the Extensible Application Markup Language (XAML), graphics processing (GPU) rendering, a layout system, data binding, styling, templating, media, and document handling. Together, they formed an amazing toolset for building the applications most developers wouldn't even think they.

With the release of .NET Framework 3.5 and Visual Studio 2008, WPF gained some new features and performance enhancements, as improved internationalization support and the capability to map two-dimensional elements onto a three-dimensional surface in an interactive manner.

However, the big feature push came with .NET Framework 3.5 SP1. Despite the Service Pack name, for WPF, this was more like a whole version up. Client profile introduced the isolation