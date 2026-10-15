# Updating a Content Control

Until now the only thing placed in your Word document was a simple graphic. While this made it apparent that you can in fact customize the content of this VSTO document, it didn’t really demonstrate the capability to dynamically update the content of the document. The first step is to look at what was one of the new features of Office 2007 — content controls. Return to the Design view of your Word document, as shown in Figure 25-18, and notice the Toolbox. Within this Toolbox is a section titled Word Controls, which has been expanded.

![](bbox=[0.094, 0.229, 0.749, 0.621])

**FIGURE 25-18**

The controls shown in this section of the Toolbox are controls that you can apply to your document. Let’s look at a couple of simple examples. Add some text similar to what is shown in Figure 25-18 (the actual content isn’t that important). Then, on a new line within the document, add the text **Document Name:** followed by a tab or two. Drag a PlainTextContentControl onto your document. On the next line, add the label **Application Name:** followed by a tab. Then drag a RichTextContentControl onto the document. These two controls will provide a simple example of working with content controls.

On the lower right-hand side of Figure 25-18, you’ll notice the Properties window. It is currently selected for the second control, but it provides an illustration of a few key content control properties. The first two are the capability to lock the control or to lock the contents of the control. Locking the control prevents users of your document from being able to delete the control. Locking the contents enables you to ensure that the text within the control can’t be modified by the user. Of the other properties shown, the Text property represents the text that should be displayed in the control, which is customized along with the Title property.

The Title property was customized to demonstrate how you can reference these controls within your code. Keep in mind that these are controls, which means you can data bind these controls to data you have retrieved, and you can handle events on these controls. Several chapters have already covered handling events, so this demo code focuses on having the actions pane interface with these controls.