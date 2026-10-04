This chapter shows you, in detail, how to create and manage your websites. It also shows you how to create your ASP.NET pages and markup to them, enabling you to create useful web pages that can present information to users and react to their responses.

Although you already created your first ASP.NET website in the previous chapter, this chapter starts with another in-depth look at creating a new website. Because you have many choices to make when you start a new site, it's important to understand all the different options and pick the right one for your scenario.

# CREATING WEBSITES WITH VISUAL STUDIO 2013

The preceding chapter gave you a quick overview of creating a website in VS. You simply chose New Web Site from the File menu, selected a language, the standard ASP.NET Web Forms template, and clicked OK. However, there is to the New Web Studio dialog box than you saw in the previous chapter. You may have noticed that you can choose among a number of different templates that enable you to create kinds of sites. Before looking at the different templates on which you can build your website, you need to know a little more about the different project types that are available in VS.

# Different Project Types

In Visual Studio 2013 you can choose between two types of projects for creating ASP.NET Web Forms websites: Web Application Projects and Web Site Projects.

# Web Application Projects

Web Application Projects make it easier for developers who work in teams or who need more control over the contents of the site and their compilation and deployment processes to build websites with VS. The whole website is managed as a project, with a single project file that keeps track of all the content of the website.

In VS, you create a new Web Application Project through the File New Project dialog box. The Web category contains a single template— ASP.NET Web Application— lets you create a web project that can contain various ASP.NET-related technologies such as Web Forms, ASP.NET MVC, and Web API. This is part of Microsoft's "One ASP.NET" initiative that aims to bring the various technologies closer together in Visual Studio. For more information about these technologies, visit www.asp.net and click the Learn menu item.

> NOTE For information on One ASP.NET, and to learn more advanced techniques, consult Professional ASP.NET 4.5 (Wrox: 978-1-11-31812-0).

# Web Site Projects

Web Site Projects represent a project in VS for a website. You create a new Web Site Project by choosing File New Web Site or File New Web from Visual Studio's main menu.