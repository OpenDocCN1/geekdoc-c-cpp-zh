![](bbox=[0.186, 0.104, 0.911, 0.549])

FIGURE 15-16　Web page after postback

Notice in Figure 15-16, that upon return from the server the Input text objects contain the typed values—unlike the illustration shown in Figure 15-15. This is because these HTML controls are now HTML server controls. The only program statements added were those added to retrieve the inputted values and display their contents in a Label object. Those statements were added to the btnSubmit_Click( ) event and previously shown in Example 15-6. No other changes were made to the .aspx.cs file. The ForeColor property for the lblOutput was set to Red using the Properties window. This caused the following statement to be added as an attribute to the Label tag:

```
ForeColor="Red"
```

It was placed in the .aspx markup file.

> **NOTE** The number displayed in the Address bar, shown in Figures 15-15 and 15-16, following local host as the port number is a relatively random number. It is placed in the Address bar when you create a Web site and specify the location as **File System**. The port number changes.