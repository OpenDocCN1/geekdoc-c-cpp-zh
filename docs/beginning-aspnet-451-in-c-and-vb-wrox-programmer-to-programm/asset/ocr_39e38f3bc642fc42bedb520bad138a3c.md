JavaScript in the Immediate window for evaluation, and so on. Also note that the Solution Explorer has changed, showing the active client-side files containing script right above the web project (see Figure 18-21).

7. To look inside these documents, you can double-click them under the Windows Internet Explorer node that has appeared in the Solution Explorer. The file WebServices.aspx should already be open in the Document Window. At first, the file may look like before. But if you look closely, you can see that this is no longer the original source file with ASP.NET controls mixed up with other markup, but the final HTML rendered in the browser. To warn you that you are looking at the final file, and not the original source, VS has added the text [dynamic] and a lock icon to the tab for the file above the Document Window, shown in Figure 18-22.

![](bbox=[0.7, 0.11, 0.92, 0.36])

FIGURE 18-21

![](bbox=[0.16, 0.42, 0.7, 0.52])

FIGURE 18-22

8. Press F5 to continue executing code. The name you entered in the text box is retrieved and then sent into the HelloWorld method of the service. Because you added a breakpoint there in step 1, the code should stop again, enabling you to look at the variable name passed to the web method. Although this exercise itself is pretty simple, a lot of magic just happened under the hood. You stepped from some client-side code running in the browser into code running in a web service at the server, all from the same IDE.

9. Press F5 again and you are taken back from the server-side web service into the client-side code where you can see the result of the web service in the helloWorldCallback handler.

10. Press F5 once more. The code completes and shows a JavaScript alert window with a greeting containing your name, just as it did in Chapter 10.

11. Press Shift+F5 to stop debugging.

# How It Works

You have a few interesting points to take away from this exercise. First of all, you should understand the notion of dynamic files, or runtime files. These files are the final result from your ASPX pages and give you insight in the final HTML, CSS, and JavaScript that ends up in the browser. This is a great help, because it gives you a total view of all relevant content. Remember, the final markup displayed in the browser comes from a variety of resources, including master pages, content pages, external CSS and