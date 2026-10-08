and ensure also see the Silverlight Version is Silverlight 4. For now

After the project has been created, the Solution Explorer. There should be a new solution, with two projects. The first is the Silverlight project, containing .xaml files (and .cs files behind them). The second project is the hosting website you created with the wizard to. It contains the HelloWorldTestPage.aspx and the HelloWorldTestPage.html pages, a JavaScript library, using Web.config, and a ClientBin directory. By building you will now see that the ClientBin folder has one item in it: the HelloWorld.xap file, which is the actual Silverlight application that gets downloaded and runs in the browser. Figure 8-2 shows how the files are laid out for your Silverlight solution.

You can also see that, after creating the solution, Visual Studio opened up the MainPage for editing, as shown in Figure 8-3.
Just as with the split view of ASP.NET, you should see a split screen, with the empty Silverlight screen on top, and the XAML code at bottom. If you don't have a split screen, click on the little horizontal line at the bottom of the editing window.

![](bbox=[0.736, 0.098, 0.918, 0.312])

FIGURE 8-2: The file structure of a Silverlight solution

![](bbox=[0.153, 0.495, 0.752, 0.903])

FIGURE 8-3: The Visual Studio 2010 workspace