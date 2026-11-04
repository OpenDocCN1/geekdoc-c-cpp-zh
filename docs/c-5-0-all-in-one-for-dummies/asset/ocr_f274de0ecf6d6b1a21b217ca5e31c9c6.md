There are others. I may have covered all the things you will see in the ToolBox, but there is a lot more out there. What you need to remember are the basics — they are visible controls with ASP.NET implementations and HTML output. You can use the property panel, the markup, or the C# code to change the properties. And you can bind them to objects in your code — which we discuss in the section “Data Binding,” later in this chapter.

# Submitting input with Submit buttons

After you get all this input into a form, you need the user to send it to you. The basic way to do this is through the Submit button.

In Chapter 1 of this minibook, I talk about the PostBack event, and how Microsoft used JavaScript to change the way the posting of forms back to the server works. The Submit button is how one does this.

Let’s be clear — any control can cause a postback. If you set an event handler for an event in a control, it will cause a postback. You can save off the form data at any point once it gets back to the server. I use the Submit button because it is what the user is used to.

The ASP.NET default controls have three buttons:

+   - **Button** is just what it says — an input of type Button submitted in HTML.
+   - **ImageButton** is a button control that has a built-in `src` property for images.
+   - **LinkButton** just shows an HTML anchor and treats it like a button.

I use one of these for nearly every page where I accept user input. Most of the time, the users expect it.

# Data Binding

Getting the data into a control in a web page isn’t enough. There needs to be some way to persist (save for reuse) that information after the data is entered. Data binding is the answer.

Data binding tells a control what member of the underlying class to get its data from. For instance, if you have a collection of `Apple` objects with a property of `Color` that you want to show in a text box, you can bind the value `Apple.Color` to the `Text` property.