that stretch beyond those of the Standard Edition, including unit testing, support for Visual Studio Tools for Office (VSTO) to extend the Office products using managed code, mobile device development, SQL database project templates, and various types of application deployment projects.

+   - Visual Studio Ultimate Edition is the collective name for the largest editions available, targeting large-scale team development. Different flavors exist, targeting various roles within a development organization, such as developers, testers, architects, and database professionals. Unique features include source control integration, rich performance analysis tools, quality metric tools, and so on. On the server side, there's Team Foundation Server (TFS), which provides the necessary infrastructure for work item tracking, source control, document libraries, project metrics reporting, and so on.

# TLA OF THE DAY: SKU

The different editions of Visual Studio—and similarly for other products—are often referred to as SKUs by Microsoft representatives. SKU is a TLA, a three-letter acronym that refers to shelve-kept unit. It comes from the days software was mostly distributed in cardboard boxes that were kept on shelves in the software store around the corner. Today, though, lots of developers get their tools through downloads, MSDN subscriptions, or enterprise agreements.

In this book, we mainly focus on language- and framework-level aspects of programming on the .NET platform, which are separate from the tooling support. However, when covering tooling support, we assume the reader has access to at least the Professional Edition of Visual Studio 2010. This said, lots of the features covered (such as debugging support to name an essential one) are available in the Express Edition, too. From time to time, we'll have a peek at Team System-level features, as well, but in a rather limited fashion.

Oh, and by the way, Visual Studio is available in different (natural) languages beyond just English. However, this book refers to the English vocabulary used in menus, dialogs, and so on.

# VISUAL STUDIO SHELL

In fact, Visual Studio is a highly extensible shell for all sorts of development and management tools. An example of a tool that's built on the Visual Studio environment is the SQL Server Management Studio. To allow the use of this infrastructure for use by third-party tools, there's the so-called Visual Studio Shell. One can go even further and embed Visual Studio capabilities in a separate application by using the Visual Studio for Applications (VSTA) platform.