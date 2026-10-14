# How to test a web application

After you design the forms and develop the code for a web application, you need to test it to be sure it works properly. Then, if you discover any errors in the application, you can debug it, correct the errors, and test it again.

In chapter 4, you'll learn all the skills you need to test and debug a web application. For now, I just want to show you how to run a web site with the built-in development server so you can test any applications that you develop for this chapter. Then, I'll show you the HTML code that's sent to the browser so you can see how that works.

# How to run a web site with the built-in development server

When you run a file-system web site by using one of the techniques in figure 2-20, Visual Studio compiles the application. If the application compiles without errors, Visual Studio automatically launches the built-in ASP.NET Development Server and displays the starting page of the web site in your default browser. Then, you can test the application to make sure that it works the way you want it to.

However, if any errors are detected as part of the compilation, Visual Studio opens the Error List window and displays the errors. These can consist of errors that have to be corrected as well as warning messages. In this figure, three errors and one warning are displayed in the Error List window.

To fix an error, you can double-click on it in the Error List window. This moves the cursor to the line of code that caused the error in the Code Editor. By moving from the Error List window to the Code Editor for all of the messages, you should be able to find the coding problems and fix them.

As you're testing an application with the development server, exceptions may occur. If an exception isn't handled by the application, ASP.NET switches to the Code Editor window and highlights the statement that caused the exception. In this case, you can end the application by clicking on the Stop Debugging button in the Debug toolbar or using the Debug➡Stop Debugging command. Then, you can fix the problem and test again.

In chapter 4, you'll learn all of the debugging skills that you'll need for more complex applications. For simple applications, though, you should be able to get by with just the skills you have right now.