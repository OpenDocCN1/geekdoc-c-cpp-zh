# Support for MVC based Web Applications

.NET Framework 4.0 and Visual Studio 2010 include the MVC framework, which enables the separation of the core business model functionality of the Web application from the presentation and control logic of the interface-specific application. This sort of arrangement makes it possible to see multiple views of the same data model of the Web application. Under this architecture, data (Model) and user interface (View) are separated from each other so that any change in the user interfaces does not affect the data in the database and vice versa.

In Visual Studio 2010, the ASP.NET MVC 2 version is installed by default. In ASP.NET 4.0, the support for MVC based Web applications helps the developers in developing standard Web applications that are easy to maintain. The support for MVC in a Web application removes the dependency among the application layers. The Web sites created using ASP.NET MVC have a modular architecture. Therefore, the developer can work on data and logic of the Web sites and the designer can work on their presentation.

# Improved CSS Compatibility

CSS is one of the important components of a Web application, as it makes the designing of a Web site easier and faster. The Visual Studio 2010 has been updated to include the improved CSS 2.1 standards. These standards are more robust than previous versions of ASP.NET and help in preserving the integrity of Web applications and their HTML code. In Visual Studio 2010, a set of tools is introduced in ASP.NET 4.0 to create, apply, and manage styles. These tools are mentioned in the following points:

+   - **Apply Styles window:** Enables you to create, modify, and apply styles. You can also link or remove an external CSS through this window.
+   - **Manage Styles window:** Helps in changing the styles in an internal style sheet. You can also use it to change or move styles inside a style sheet.
+   - **CSS Properties window:** Shows the styles in a Web page that are currently in use. It also displays the priority order of the styles. The CSS Properties window displays the list of all the CSS properties. It enables you to add more properties to an existing style and modify the properties that you have already set. In addition, this window helps you in creating new inline styles.
+   - **Direct Style Application toolbar:** Enables you to apply class-based or ID-based style. It helps you to create and apply new styles. It can also be used to remove class-based or ID-based styles. It also controls the new styles generated.

After learning about new features of ASP.NET 4.0, now let’s learn about Web application in ASP.NET 4.0.

# Exploring ASP.NET 4.0 Web Application

In ASP.NET 4.0, you can create both Web applications and Web sites with each having its own advantages. For example, MVC and some tools for automation of Web deployment work only with Web application projects. The Dynamic Data feature, which is new in this version of ASP.NET, works with both Web sites and Web application projects.

Table 1.1 lists the main differences between a Web application and Web site project:

| Area | Web Application | Web Site |
|---|---|---|
| Structure of project file (.csproj or .vbproj) | Stores information about the list of files that are included in the ASP.NET project. | Consists of no project file, therefore, you cannot double click to open the Web site directly. The files are included automatically in the Web site. |
| Compilation | Requires you to build the project in Visual Studio. In the process of compilation of the application, the class | Does not require you to manually compile the project. The Web site is compiled dynamically by ASP.NET, which produces multiple assemblies. |