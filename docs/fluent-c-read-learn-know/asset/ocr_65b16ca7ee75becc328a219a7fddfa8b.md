# # XAML

Well, we've learned about the .NET environment and the C# programming language. and we've taken a quick look at some of the principles and practices that will help you make your programs efficient and resilient. Now it's time to return to the .NET Framework and get our hands dirty with one of the FCL technologies.

We're going to look at Windows Presentation Foundation (WPF), one of the two .NET technologies that you can use to develop applications for the Windows desktop.

Now, before you stop reading because you're not interested in Windows desktop applications, let me assure you that the reason I chose WPF as the technology to explore is that the concepts and techniques you'll learn in studying WPF will be useful in most of the other .NET technology areas. Silverlight, for example, which is used for developing Rich Internet Applications and Phone 7 apps, is basically a subset of WPF, and the integration of an XML-based language with C# is fundamental to most of Microsoft's new technologies.

It's that XAML and code integration that we're going to examine in this chapter. XAML (pronounced "zammel", which rhymes with "camel"), is the declarative language that's used to describe the layout of a WPF window. It's based on XML (XAML is actually an acronym for "Xnl Application Markup Language") and allows you to separate the appearance of an application (defined in the XAML) from its behavior (defined in code-behind.)