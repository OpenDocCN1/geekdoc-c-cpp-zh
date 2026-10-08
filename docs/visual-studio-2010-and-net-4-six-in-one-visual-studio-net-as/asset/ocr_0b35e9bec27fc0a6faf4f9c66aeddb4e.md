# Other Features

There are a lot of Silverlight features not yet examined. However, because this chapter is just an introduction to WPF and Silverlight, these features will only get a few paragraphs of coverage, despite the fact that entire chapters (or even books) could be written about some of them.

# Out-of-Browser (OOB) Applications

Silverlight applications mostly live in the browser as plug-ins. However, Silverlight supports applications out of the browser, and onto the desktop. Installing out-of-browser (OOB) applications is always a user-initiated process — either by right-clicking the Silverlight application and choosing "Install <appname> to this computer," or by clicking on a developer-created piece of UI that calls the Application.Install method. Either way, the user is prompted whether or she really wants to install the application, and whether the installer should create a shortcut on the Desktop or Start Menu.

By default, OOB applications run within the same sandbox as the browser, so no user account (UAC) prompts are necessary. OOB applications work on OS X as well, so here is a great way to create OS desktop applications without even running a Mac!

Some features are only available in OOB mode. These include the WebBrowser control and the HtmlBrush control. The WebBrowser is a full-featured web browser that can be used as a rectangular frame within the Silverlight application, and any web page or HTML content (including websites that have other Silverlight, or even Flash, plug-ins). HTMLBrush is similar to VideoBrush. When attached to a WebBrowser control it can be used as a brush for any UI element. However, the WebBrowser control remains interactive and accepts keyboard and mouse input, the VideoBrush handles the interactivity.

OOB applications can also be installed with elevated privileges. Figure 8-36 shows OOB settings in Visual Studio 2010. Elevated privileges enable the need from cross-domain policy files, and allow reading from or sending information to any website; give access to files and directories within the My Documents folder; and allow a level of COM interoperability, so that Office automation can be denied.

![](bbox=[0.548, 0.452, 0.931, 0.833])

FIGURE 8-36: Silverlight OOB Settings in Visual Studio