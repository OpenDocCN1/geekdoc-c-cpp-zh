> Chapter 6 discusses in detail the Visual Studio SDK, and shows several examples of its application, including Visual Studio Packages and Editor extensions. You can download Visual Studio 2010 SDK through the Visual Studio Development Center (http://msdn.com/vsx). It is about 12 MB. Its installation is straightforward and takes two minutes.

Microsoft created a Visual Studio project template to develop Start Pages. The first time you want to create a project with this template, select the File -> New Project command to develop the New Project. Click the Online Templates tab and select the Visual Extensions category. In this category, you can locate the Custom Start Page Project template, as shown in Figure 5-26.

![](bbox=[0.095, 0.355, 0.855, 0.683])

FIGURE 5-26: Locating the Custom Start Page Project Template

Name the project SimpleStartPage. When you click OK, Visual Studio downloads the project and starts installing, asking you for confirmation. After you confirm the installation, the project is created. The next time you want to create a Start Page, you will find the template under the Installed Templates tab, so you do not have to download it.

Build and run the project without debugging by pressing Ctrl+F5. When you start it, a new instance of Visual Studio (the Experimental Instance) is launched, and it opens the default Start Page. Go to Tools -> Options and select the Start page option under the Environment category, as shown in Figure 5-25. Now drop down the Custom Start Page combo box and select [Installed Extension]. When you click OK, the page is changed to the one that is implemented by the SimpleStartPage project, as shown in Figure 5-27.