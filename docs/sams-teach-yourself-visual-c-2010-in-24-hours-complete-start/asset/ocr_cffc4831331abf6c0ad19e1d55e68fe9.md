# # Understanding WPF

Windows Presentation Foundation (WPF) provides a unified programming model enabling you to build Windows applications that incorporate user interface elements, media, and documents. WPF, however, goes beyond just user interfaces. It is a next-generation presentation system enabling you to create a wide range of visually rich standalone and browser-hosted applications. At the center of WPF is a resolution-independent vector-based rendering engine designed to take advantage of modern graphics hardware. WPF is part of the .NET Framework and most of the types you need are located in the `System.Windows` namespace.

# ## Working with Markup and Code-Behind

If you have previously developed ASP.NET applications, the idea of markup and code-behind should already be familiar. In a WPF application, you use a markup language to implement the appearance of the application; you implement the behavior using a programming language, such as C#, “behind” the markup. This enables a clean separation between appearance and behavior, providing the following benefits:

+   - Reduced development and maintenance cost.
- Development is more efficient, allowing the application’s appearance to be created simultaneously with other developers who are implementing the application’s behavior.
- Multiple design tools can create and share the markup.

# ## Markup

WPF uses Extensible Application Markup Language (XAML), which is an XML-based compositional markup language. Because XAML is XML-based, the user interface (UI) you compose with it is assembled in an element tree, which is a hierarchy of nested elements. The element tree provides a logical way to create and manage the user interface.

Figure 17.1 shows a simple WPF application written completely in XAML. Specifically, the XAML defines a window and a button using the Window and Button elements, respectively, and then sets various attributes to specify the text, sizes, and so on.

![](bbox=[0.39, 0.81, 0.68, 0.91])

FIGURE 17.1
“Hello World”
in WPF