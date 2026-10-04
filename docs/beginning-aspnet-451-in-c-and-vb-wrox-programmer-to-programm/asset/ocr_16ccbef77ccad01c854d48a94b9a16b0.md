# USING ASP.NET AJAX IN YOUR PROJECTS

ASP.NET AJAX is fully integrated in ASP.NET and VS, which means you can start it right away. Each new ASP.NET 4.5.1 web project you create in VS is already Ajax-enabled. In addition, the Toolbox contains an AJAX Extensions gallery with a number of Ajax-related controls that you can use in your pages. Visual Studio has great support for ASP.NET AJAX, giving you IntelliSense for the controls as well as for the client-side JavaScript you'll write to interact with the client page and code running on the server.

# Creating Flicker-free Pages

To avoid full postbacks in your ASPX pages you can use only part of the page, use the UpdatePanel control. For this to operate correctly, you also need a ScriptManager control. If you're going to use functionality in many of your ASPX pages, you can place the ScriptManager in the master page, so it's available in all pages that are managed by this master. You have only one ScriptManager per page, so if you add one to master page, you can't add another to a content page. To access a ScriptManager control that is defined in a master page from a content page, you can use the ScriptManagerProxy control as explained. You'll find these other Ajax-related controls in the AJAX Extensions gallery of the Toolbox, shown in Figure 10-2.

![](bbox=[0.718, 0.303, 0.853, 0.483])

The following two sections introduce you to the UpdatePanel and ScriptManager controls. After the introduction you will learn how to use these controls in the pages of your Planet Wrox website. Later sections introduce you to the UpdateProgress, Timer, and ScriptManager Proxy controls.

# The UpdatePanel Control

The UpdatePanel control is a key component in creating flicker-free pages. In its most basic application, you wrap the control over content you want to update, add a ScriptManager to the page, and when one of the controls within the UpdatePanel causes a postback to the server, only the content within that UpdatePanel is refreshed.

To see what problems the UpdatePanel control solves and how it behaves in a client page, the following Try It Out shows a simple example that uses the panel to avoid page flicker during postbacks.

# TRY IT OUT Adding an UpdatePanel to a Page

In this exercise, you add a Label and a button to a page. When you click the button in the browser, the Text property of the Label is updated with the current date and time at the server. To avoid the page flicker typically associated with postbacks, you then wrap the controls in an UpdatePanel to see how that affects the behavior.

+   1. Open the Planet Wrox website in Visual Studio.
2. In the Demos folder, create a new Web Form UpdatePanel.aspx using your custom template. Give the page a Title of UpdatePanel Demo.