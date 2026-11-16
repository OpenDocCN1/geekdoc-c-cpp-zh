![](bbox=[0.153, 0.103, 0.532, 0.278])

Figure 9.12 Importing the Weather Widget Content: Part 2

After the content is imported, you should see (among other things) two new files: weather.html and weather.spec.xml. With these files in place, you can delete the original HTML and spec XML files, because they're superseded by the imported files.

# Developing the Weather Widget's Content

If you open the weather.html file that contains the weather widget's content, you'll find that it looks pretty much any other HTML5 source file. Aside from the JavaScript script content (which we'll return to in Section 9.3.2), you'll find that the HTML <body> section consists of two <div> tags that are used to render the content shown in Figure 9.13. As you can see, the left-hand side of the content area shows the current temperature, whereas the right-hand side contains a REFRESH button, which allows users to refresh the current temperature value for their location.

![](bbox=[0.153, 0.673, 0.453, 0.813])

Figure 9.13 Demonstration of the Widget in Use in a Portal Site Definition