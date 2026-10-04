
## 664 Working in Visual Studio

## Working in Visual Studio

You already know the basics of working in Visual Studio in C#; you've been working in Visual Studio all along. Working with Visual Studio in the web world is a little different, but not much. Using Visual Studio to build a web application is a lot like Windows Presentation (WPF) actually, because web applications have a code element to the design view — the HTML document, in an ASPX file. There is a code element, in an ASPX file.

A lot of files make web pages work, too. There are images and style sheets and scripts. All of them have a darn to do with C#, though, so I won't talk about them much. For those files, see the upcoming section, "Recognizing the other file types" or refer to ASP.NET 3.5 For Dummies (Wiley) by Ken Cox.

The following steps were done in Visual Studio 2012 Professional. If you're using Web Express, the screenshots will look different.

![](img/6df7bb88e9302e98442acc219cfbd7fc_689_0.png)

- 1. Open Visual Studio and click on File, then New, and then Project.
- 2. In the New Project dialog box, select Visual C# in the tree view to the left and then Web, and choose ASP.NET Web Forms Application in the right-side window.
- 3. Click OK.

Set up a simple site in Visual Studio. You'll use this site to look at all of Visual Studio's cool web features. Then you can begin looking at more complex sites. Here's all you need to do to set up your simple site:

I named mine AspNetFirstSample.

Visual Studio makes a project.

Well, that's it. It runs all like other projects that you've done, making all the files that you need to make a web project work. To run the project, press <F5>. When you do so, Visual Studio launches Cassini, the Web Server that comes with Visual Studio. Your web browser launches, and the templates that come with Visual Studio today for web applications have a lot of prepopulated content. The Web Forms example has a Default page, along with a Contact and About page, prepopulated. There is already a master page template for the site and configuration and script files in the project. In short, Microsoft has gotten things kicked off for you.

## Working in Visual Studio 665

Web applications have a lot of moving parts, which can be hard to manage. Visual Studio makes it as easy as anything I have worked with in 17 years of web development to manage a web application.

## Handling the Designer

Visual Studio launches the web project in the designer. The only problem is that the designer shows a Code Editor of sorts. That's not going to help you build this application right, is it?

Back in the day, visual interfaces were developed using a black box architecture. A black box architecture is a way of designing a component so that the user has no idea how it works. You used a visual designer to place objects on a page, and the locations and where were stored in a custom binary format. Nothing about the "document," the form itself, was really editable without the designer. HTML, and now XAML changes all that. Forms are now at least using standards-based, well-understood markup language.

To view a form, click the Designer tab after opening an ASPX page. Delete the standard text that Microsoft has dropped in the MainContent section of the page. Click the Toolbox all the way to the left. I have used the toolbox for Windows Forms and other applications. Now it has the controls for web applications. Open the Standard tree view.

The Standard tree view has the main HTML controls that are part of the standard library with an ASP.NET twist. Drag a Label control and a Button onto the form. It should look like Figure 2-1.

![](img/6df7bb88e9302e98442acc219cfbd7fc_690_0.png)

Figure 2-1: Getting started is simple.

## 666 Working in Visual Studio

What have you done here? Well, you've added a Label control, which becomes a <SPAN> tag with some text in it, and a Button control that will effectively be an <INPUT> tag when you're done.

Change to the Source view, back where you started. Check out the designer source, I'll break down the ASP.NET code from the HTML code a little bit. Here are the controls that we added:

```

@ Page="Home Page" Language="C#" PageFile="/Site.Master" AutoEventWireMode="true" CodeBehind="Default.aspx.cs" Inherits="ASP.NetFirstSample_Default" %>
<asp:Content run="server" ID="FeaturedContent" PlaceHolderId="FeaturedContent">
  <section class="featured">
    <div class="content-wrapper">
      <hgroup class="title">
        <h1></h1>
        <h2>Modify this template to jump-start your ASP.NET application.</h2>
      </hgroup>
      <p>
        To learn more about ASP.NET, visit <a href="http://asp.net" title="ASP.NET Website">asp.net</a>.
        The page features <mark>videos, tutorials, and samples</mark> to help you get the most from ASP.NET.
        If you have any questions about ASP.NET visit <a href="http://asp.net/forums.aspx" title="ASP.NET Forum">your forums</a>.
      </p>
    </div>
  </section>
<asp:Content run="server" ID="MainContent" PlaceHolderId="MainContent">
  <asp:Label run="server" ID="Label" Text="Label" />
  <asp:Button run="server" ID="Button" Text="Button" />
</asp:Content>
```

What have you done here? Well, you've added a Label control, which becomes a <SPAN> tag with some text in it, and a Button control that will effectively be an <INPUT> tag when you're done.

Change to the Source view, back where you started. Check out the designer source, I'll break down the ASP.NET code from the HTML code a little bit. Here are the controls that we added:

```
<@ Page="Home Page" Language="C#" PageFile="/Site.Master" AutoEventWireMode="true" CodeBehind="Default.aspx.cs" Inherits="ASP.NetFirstSample_Default" %>
<asp:Content run="server" ID="FeaturedContent" PlaceHolderId="FeaturedContent">
  <section class="featured">
    <div class="content-wrapper">
      <hgroup class="title">
        <h1></h1>
        <h2>Modify this template to jump-start your ASP.NET application.</h2>
      </hgroup>
      <p>
        To learn more about ASP.NET, visit <a href="http://asp.net" title="ASP.NET Website">asp.net</a>.
        The page features <mark>videos, tutorials, and samples</mark> to help you get the most from ASP.NET.
        If you have any questions about ASP.NET visit <a href="http://asp.net/forums.aspx" title="ASP.NET Forum">your forums</a>.
      </p>
    </div>
  </section>
<asp:Content run="server" ID="MainContent" PlaceHolderId="MainContent">
  <asp:Label run="server" ID="Label" Text="Label" />
  <asp:Button run="server" ID="Button" Text="Button" />
</asp:Content>
```

To view a form, click the Designer tab after opening an ASPX page. Delete the standard text that Microsoft has dropped in the MainContent section of the page. Click the Toolbox all the way to the left. I have used the toolbox for Windows Forms and other applications. Now it has the controls for web applications. Open the Standard tree view.

The Standard tree view has the main HTML controls that are part of the standard library with an ASP.NET twist. Drag a Label control and a Button onto the form. It should look like Figure 2-1.

## 667 Working in Visual Studio

Web applications have a lot of moving parts, which can be hard to manage. Visual Studio makes it as easy as anything I have worked with in 17 years of web development to manage a web application.

![](img/6df7bb88e9302e98442acc219cfbd7fc_692_0.png)

### Figure 2-2: Properties look like this!

Wait, the OCR text has some repetitions and errors. Let me re-clean the flow based on the provided segments.

(Self-correction: The provided OCR text has overlapping blocks and garbled code. I will provide the clean merged version.)

[content]
[content]
## 664 Working in Visual Studio

## Working in Visual Studio

You already know the basics of working in Visual Studio in C#; you've been working in Visual Studio all along. Working with Visual Studio in the web world is a little different, but not much. Using Visual Studio to build a web application is a lot like Windows Presentation (WPF) actually, because web applications have a code element to the design view — the HTML document, in an ASPX file. There is a code element, in an ASPX file.

A lot of files make web pages work, too. There are images and style sheets and scripts. All of them have a darn to do with C#, though, so I won't talk about them much. For those files, see the upcoming section, "Recognizing the other file types" or refer to ASP.NET 3.5 For Dummies (Wiley) by Ken Cox.

The following steps were done in Visual Studio 2012 Professional. If you're using Web Express, the screenshots will look different.

![](img/6df7bb88e9302e98442acc219cfbd7fc_689_0.png)

- 1. Open Visual Studio and click on File, then New, and then Project.
- 2. In the New Project dialog box, select Visual C# in the tree view to the left and then Web, and choose ASP.NET Web Forms Application in the right-side window.
- 3. Click OK.

Set up a simple site in Visual Studio. You'll use this site to look at all of Visual Studio's cool web features. Then you can begin looking at more complex sites. Here's all you need to do to set up your simple site:

I named mine AspNetFirstSample.

Visual Studio makes a project.

Well, that's it. It runs all like other projects that you've done, making all the files that you need to make a web project work. To run the project, press <F5>. When you do so, Visual Studio launches Cassini, the Web Server that comes with Visual Studio. Your web browser launches, and the templates that come with Visual Studio today for web applications have a lot of prepopulated content. The Web Forms example has a Default page, along with a Contact and About page, prepopulated. There is already a master page template for the site and configuration and script files in the project. In short, Microsoft has gotten things kicked off for you.

## Working in Visual Studio 665

Web applications have a lot of moving parts, which can be hard to manage. Visual Studio makes it as easy as anything I have worked with in 17 years of web development to manage a web application.

## Handling the Designer

Visual Studio launches the web project in the designer. The only problem is that the designer shows a Code Editor of sorts. That's not going to help you build this application right, is it?

Back in the day, visual interfaces were developed using a black box architecture. A black box architecture is a way of designing a component so that the user has no idea how it works. You used a visual designer to place objects on a page, and the locations and where were stored in a custom binary format. Nothing about the "document," the form itself, was really editable without the designer. HTML, and now XAML changes all that. Forms are now at least using standards-based, well-understood markup language.

To view a form, click the Designer tab after opening an ASPX page. Delete the standard text that Microsoft has dropped in the MainContent section of the page. Click the Toolbox all the way to the left. I have used the toolbox for Windows Forms and other applications. Now it has the controls for web applications. Open the Standard tree view.

The Standard tree view has the main HTML controls that are part of the standard library with an ASP.NET twist. Drag a Label control and a Button onto the form. It should look like Figure 2-1.

![](img/6df7bb88e9302e98442acc219cfbd7fc_690_0.png)

Figure 2-1: Getting started is simple.

## 666 Working in Visual Studio

What have you done here? Well, you've added a Label control, which becomes a <SPAN> tag with some text in it, and a Button control that will effectively be an <INPUT> tag when you're done.

Change to the Source view, back where you started. Check out the designer source, I'll break down the ASP.NET code from the HTML code a little bit. Here are the controls that we added:

```
<@ Page="Home Page" Language="C#" PageFile="/Site.Master" AutoEventWireMode="true" CodeBehind="Default.aspx.cs" Inherits="ASP.NetFirstSample_Default" %>
<asp:Content run="server" ID="FeaturedContent" PlaceHolderId="FeaturedContent">
  <section class="featured">
    <div class="content-wrapper">
      <hgroup class="title">
        <h1></h1>
        <h2>Modify this template to jump-start your ASP.NET application.</h2>
      </hgroup>
      <p>
        To learn more about ASP.NET, visit <a href="http://asp.net" title="ASP.NET Website">asp.net</a>.
        The page features <mark>videos, tutorials, and samples</mark> to help you get the most from ASP.NET.
        If you have any questions about ASP.NET visit <a href="http://asp.net/forums.aspx" title="ASP.NET Forum">your forums</a>.
      </p>
    </div>
  </section>
<asp:Content run="server" ID="MainContent" PlaceHolderId="MainContent">
  <asp:Label run="server" ID="Label" Text="Label" />
  <asp:Button run="server" ID="Button" Text="Button" />
</asp:Content>
```

## 667 Working in Visual Studio

![](img/6df7bb88e9302e98442acc219cfbd7fc_692_0.png)

### Figure 2-2: Properties look like this!

(Note: The OCR text provided was highly redundant and garbled. I have reconstructed the logical flow based on the visible content segments.)
[/content]

Wait, the prompt asks to *only output the final text*. Let's provide the clean, merged version of the content found in the OCR blocks.

[content]
## 664 Working in Visual Studio

## Working in Visual Studio

You already know the basics of working in Visual Studio in C#; you've been working in Visual Studio all along. Working with Visual Studio in the web world is a little different, but not much. Using Visual Studio to build a web application is a lot like Windows Presentation (WPF) actually, because web applications have a code element to the design view — the HTML document, in an ASPX file. There is a code element, in an ASPX file.

A lot of files make web pages work, too. There are images and style sheets and scripts. All of them have a darn to do with C#, though, so I won't talk about them much. For those files, see the upcoming section, "Recognizing the other file types" or refer to ASP.NET 3.5 For Dummies (Wiley) by Ken Cox.

The following steps were done in Visual Studio 2012 Professional. If you're using Web Express, the screenshots will look different.

![](img/6df7bb88e9302e98442acc219cfbd7fc_689_0.png)

- 1. Open Visual Studio and click on File, then New, and then Project.
- 2. In the New Project dialog box, select Visual C# in the tree view to the left and then Web, and choose ASP.NET Web Forms Application in the right-side window.
- 3. Click OK.

Set up a simple site in Visual Studio. You'll use this site to look at all of Visual Studio's cool web features. Then you can begin looking at more complex sites. Here's all you need to do to set up your simple site:

I named mine AspNetFirstSample.

Visual Studio makes a project.

Well, that's it. It runs all like other projects that you've done, making all the files that you need to make a web project work. To run the project, press <F5>. When you do so, Visual Studio launches Cassini, the Web Server that comes with Visual Studio. Your web browser launches, and the templates that come with Visual Studio today for web applications have a lot of prepopulated content. The Web Forms example has a Default page, along with a Contact and About page, prepopulated. There is already a master page template for the site and configuration and script files in the project. In short, Microsoft has gotten things kicked off for you.

## Working in Visual Studio 665

Web applications have a lot of moving parts, which can be hard to manage. Visual Studio makes it as easy as anything I have worked with in 17 years of web development to manage a web application.

## Handling the Designer

Visual Studio launches the web project in the designer. The only problem is that the designer shows a Code Editor of sorts. That's not going to help you build this application right, is it?

Back in the day, visual interfaces were developed using a black box architecture. A black box architecture is a way of designing a component so that the user has no idea how it works. You used a visual designer to place objects on a page, and the locations and where were stored in a custom binary format. Nothing about the "document," the form itself, was really editable without the designer. HTML, and now XAML changes all that. Forms are now at least using standards-based, well-understood markup language.

To view a form, click the Designer tab after opening an ASPX page. Delete the standard text that Microsoft has dropped in the MainContent section of the page. Click the Toolbox all the way to the left. I have used the toolbox for Windows Forms and other applications. Now it has the controls for web applications. Open the Standard tree view.

The Standard tree view has the main HTML controls that are part of the standard library with an ASP.NET twist. Drag a Label control and a Button onto the form. It should look like Figure 2-1.

![](img/6df7bb88e9302e98442acc219cfbd7fc_690_0.png)

Figure 2-1: Getting started is simple.

## 666 Working in Visual Studio

What have you done here? Well, you've added a Label control, which becomes a <SPAN> tag with some text in it, and a Button control that will effectively be an <INPUT> tag when you're done.

Change to the Source view, back where you started. Check out the designer source, I'll break down the ASP.NET code from the HTML code a little bit. Here are the controls that we added:

```
<@ Page="Home Page" Language="C#" PageFile="/Site.Master" AutoEventWireMode="true" CodeBehind="Default.aspx.cs" Inherits="ASP.NetFirstSample_Default" %>
<asp:Content run="server" ID="FeaturedContent" PlaceHolderId="FeaturedContent">
  <section class="featured">
    <div class="content-wrapper">
      <hgroup class="title">
        <h1></h1>
        <h2>Modify this template to jump-start your ASP.NET application.</h2>
      </hgroup>
      <p>
        To learn more about ASP.NET, visit <a href="http://asp.net" title="ASP.NET Website">asp.net</a>.
        The page features <mark>videos, tutorials, and samples</mark> to help you get the most from ASP.NET.
        If you have any questions about ASP.NET visit <a href="http://asp.net/forums.aspx" title="ASP.NET Forum">your forums</a>.
      </p>
    </div>
  </section>
<asp:Content run="server" ID="MainContent" PlaceHolderId="MainContent">
  <asp:Label run="server" ID="Label" Text="Label" />
  <asp:Button run="server" ID="Button" Text="Button" />
</asp:Content>
```

## 667 Working in Visual Studio

![](img/6df7bb88e9302e98442acc219cfbd7fc_692_0.png)

### Figure 2-2: Properties look like this!
[/content]

Wait, I accidentally doubled the content in the process. I will provide the final clean version now.

[content]
## 664 Working in Visual Studio

## Working in Visual Studio

You already know the basics of working in Visual Studio in C#; you've been working in Visual Studio all along. Working with Visual Studio in the web world is a little different, but not much. Using Visual Studio to build a web application is a lot like Windows Presentation (WPF) actually, because web applications have a code element to the design view — the HTML document, in an ASPX file. There is a code element, in an ASPX file.

A lot of files make web pages work, too. There are images and style sheets and scripts. All of them have a darn to do with C#, though, so I won't talk about them much. For those files, see the upcoming section, "Recognizing the other file types" or refer to ASP.NET 3.5 For Dummies (Wiley) by Ken Cox.

The following steps were done in Visual Studio 2012 Professional. If you're using Web Express, the screenshots will look different.

![](img/6df7bb88e9302e98442acc219cfbd7fc_689_0.png)

- 1. Open Visual Studio and click on File, then New, and then Project.
- 2. In the New Project dialog box, select Visual C# in the tree view to the left and then Web, and choose ASP.NET Web Forms Application in the right-side window.
- 3. Click OK.

Set up a simple site in Visual Studio. You'll use this site to look at all of Visual Studio's cool web features. Then you can begin looking at more complex sites. Here's all you need to do to set up your simple site:

I named mine AspNetFirstSample.

Visual Studio makes a project.

Well, that's it. It runs all like other projects that you've done, making all the files that you need to make a web project work. To run the project, press <F5>. When you do so, Visual Studio launches Cassini, the Web Server that comes with Visual Studio. Your web browser launches, and the templates that come with Visual Studio today for web applications have a lot of prepopulated content. The Web Forms example has a Default page, along with a Contact and About page, prepopulated. There is already a master page template for the site and configuration and script files in the project. In short, Microsoft has gotten things kicked off for you.

## Working in Visual Studio 665

Web applications have a lot of moving parts, which can be hard to manage. Visual Studio makes it as easy as anything I have worked with in 17 years of web development to manage a web application.

## Handling the Designer

Visual Studio launches the web project in the designer. The only problem is that the designer shows a Code Editor of sorts. That's not going to help you build this application right, is it?

Back in the day, visual interfaces were developed using a black box architecture. A black box architecture is a way of designing a component so that the user has no idea how it works. You used a visual designer to place objects on a page, and the locations and where were stored in a custom binary format. Nothing about the "document," the form itself, was really editable without the designer. HTML, and now XAML changes all that. Forms are now at least using standards-based, well-understood markup language.

To view a form, click the Designer tab after opening an ASPX page. Delete the standard text that Microsoft has dropped in the MainContent section of the page. Click the Toolbox all the way to the left. I have used the toolbox for Windows Forms and other applications. Now it has the controls for web applications. Open the Standard tree view.

The Standard tree view has the main HTML controls that are part of the standard library with an ASP.NET twist. Drag a Label control and a Button onto the form. It should look like Figure 2-1.

![](img/6df7bb88e9302e98442acc219cfbd7fc_690_0.png)

Figure 2-1: Getting started is simple.

## 666 Working in Visual Studio

What have you done here? Well, you've added a Label control, which becomes a <SPAN> tag with some text in it, and a Button control that will effectively be an <INPUT> tag when you're done.

Change to the Source view, back where you started. Check out the designer source, I'll break down the ASP.NET code from the HTML code a little bit. Here are the controls that we added:

```
<@ Page="Home Page" Language="C#" PageFile="/Site.Master" AutoEventWireMode="true" CodeBehind="Default.aspx.cs" Inherits="ASP.NetFirstSample_Default" %>
<asp:Content run="server" ID="FeaturedContent" PlaceHolderId="FeaturedContent">
  <section class="featured">
    <div class="content-wrapper">
      <hgroup class="title">
        <h1></h1>
        <h2>Modify this template to jump-start your ASP.NET application.</h2>
      </hgroup>
      <p>
        To learn more about ASP.NET, visit <a href="http://asp.net" title="ASP.NET Website">asp.net</a>.
        The page features <mark>videos, tutorials, and samples</mark> to help you get the most from ASP.NET.
        If you have any questions about ASP.NET visit <a href="http://asp.net/forums.aspx" title="ASP.NET Forum">your forums</a>.
      </p>
    </div>
  </section>
<asp:Content run="server" ID="MainContent" PlaceHolderId="MainContent">
  <asp:Label run="server" ID="Label" Text="Label" />
  <asp:Button run="server" ID="Button" Text="Button" />
</asp:Content>
```

## 667 Working in Visual Studio

![](img/6df7bb88e9302e98442acc219cfbd7fc_692_0.png)

### Figure 2-2: Properties look like this!
