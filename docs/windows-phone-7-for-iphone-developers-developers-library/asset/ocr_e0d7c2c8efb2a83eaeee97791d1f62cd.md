the next time you see a Microsoft evangelist or group product manager, make sure you yell at them and complain about the sad state of affairs when it comes to their unit testing capabilities on Windows Phone 7.

However, unit testing is still possible and relatively painless, depending on the approach you take. The following section walks you through the various ways you can get unit testing to work on Windows Phone 7. I also provide my recommended approach (at least the one I recommend given the tools available to me at the time I wrote this book).

# Working with nUnit

Several guides available on the Internet at the moment explain various ways to get nUnit working for Windows Phone 7. In general, what you do is this:

+   - Download a Silverlight 3 port of the nUnit 2.5.5 library.
+   - Download the Silverlight Unit Test Framework, a part of the full Silverlight (not WP7!) version of the Silverlight Toolkit available from silverlight.codeplex.com.
+   - Create a new Silverlight Unit Test application and drop the framework target from Silverlight 4 to Silverlight 3.
+   - Add references to the Silverlight 3 ported versions of the nUnit assemblies.
+   - Add a reference to the WP7 application from the Silverlight unit test framework.
+   - This is where it gets fun: Unload the Silverlight project, edit the .csproj file, and manually edit the ProjectTypeGuids XML element so that VS2010 will allow references to WP7 projects and class libraries.
+   - Make some adjustments to the metadata configuration of the Silverlight Unit Test Framework so that it will execute nUnit tests instead of Microsoft Test (MSTest) tests.
+   - If you’ve managed to do all this without messing anything up, in theory you can use nUnit to execute tests against your Silverlight application. However, it isn’t always that easy, and the presence of references like GalaSoft’s MVVM Light framework only serves to complicate things further.

For this last reason, among many others, I don’t recommend that you bother with trying to get nUnit tests working on Windows Phone 7. I am a huge fan of the nUnit test framework, and in general I prefer it to that of the MSTest framework. However, the tooling and integration support for Windows Phone 7 are just not available at the moment.

The other thing I don’t like about this approach is that the test execution environment is a real Silverlight environment. Despite the hackery done to the Visual Studio projects, it is still possible that the tests you write could attempt to do something that isn’t possible in a Windows Phone 7 application and your tests will still pass. I much prefer executing my unit tests in a true WP7 environment, as I’ll show in the next section.

If, by the time you have purchased and read this book, the native support for nUnit on WP7 has gotten better, easier to use, and more integrated into Visual Studio, by all means feel free to use that as your testing framework of choice.