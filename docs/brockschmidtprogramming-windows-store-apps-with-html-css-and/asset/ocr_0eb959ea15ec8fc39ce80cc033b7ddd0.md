# Sidebar: How Does Visual Studio Run an App?

Under the covers, Visual Studio is actually deploying the app similar to what would happen if you acquired it from the Store. The app will show up on the Start screen's All Apps view, where you can also uninstall it. Uninstalling will clear out appdata folders and other state, which is very helpful when debugging.

There's no magic involved: deployment can actually be done through the command line. To see the details, use the Store/Create App Package in Visual Studio, select No for a Store upload, and you'll see a dialog in which you can save your package to a folder. In that folder you'll then find an appx package, a security certificate, and a batch file called Add-AppxDevPackage. That batch file contains PowerShell scripts that will deploy the app along with its dependencies.

These same files are also what you can share with other developers who have a developer license, allowing them to side-load your app without needing your full source project.

# Blank App Project Structure

Although an app created with the Blank template doesn't offer much in the visual department, it lets us see the core structure of all projects you'll use. That structure is found in Visual Studio's Solution Explorer (as shown in Figure 2-6).

In the project root folder:

+   - default.html The starting page for the app.
+   - <Appname>_TemporaryKey.pfx A temporary signature created on first run.
+   - package.appxmanifest The manifest. Opening this file will display Visual Studio's manifest editor (shown later in this chapter). Browse around in this UI for a few minutes to familiarize yourself with what's here: references to the various app images (see below), a checkmark on the Internet (Client) capability, default.html selected as the start page, and all the places where you control different aspects of your app. We'll be seeing these throughout this book; for a complete reference, see the App packages and deployment and Using the manifest designer topics. And if you want to explore the manifest XML directly, right-click this file and select View Code. This is occasionally necessary to configure uncommon options that aren't represented in the editor UI. The APIs for accessing package details are demonstrated in the App package information sample.

The css folder contains a default.css file that's empty except for a blank rule for the body element.

The images folder contains four placeholder branding images, and unless you want to look like a real doofus developer, always customize these before sending your app to the Store (and to provide scaled versions too, as we'll see in Chapter 3, "App Anatomy and Performance Fundamentals"):