# Using other kinds of input controls

ASP.NET provides a number of other input types that are combinations of the above, or are nontraditional inputs (see Figure 3-5). They are all special-use controls, but they need to be in your toolbox so that you can use them when the need arises.

They include the following input types:

+   - **FileUpload:** The FileUpload does exactly what it says. It creates an HTML input of type File and makes the form *enctype* (encoding type) into multipart form-data. This allows the web server to accept a long stream of binary data, which you can then capture with a streamreader.
+   - **Imagemaps:** Imagemaps are nearly relics of a bygone era. Essentially, they allow you to mark off pixel by pixel maps on top of images and then assign regions within those maps to URLs or other actions. This control assists you by giving you the framework. You still have to provide the map. Now, usually people use separate images.
+   - **Calendars:** The calendar control is just a textbox that helps the user format dates properly. It works well. There are a ton of formatting options, too — check them out in the property panel.

![](bbox=[0.253, 0.523, 0.876, 0.868])