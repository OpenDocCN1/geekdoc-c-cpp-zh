# Part II: Application Development Using C#

![](bbox=[0.18, 0.11, 0.78, 0.44])

Figure 18-9

These images will be used by the TreeView control to display its content when the tree is expanded or closed. Hence, associate the ImageList control to the TreeView control by setting the ImageList property of the TreeView control to ImageList1.

Add a new Windows Form to the project, and populate it with a WebBrowser and MenuItem control (see Figure 18-10). The WebBrowser control will be used to view the content of a posting.

![](bbox=[0.22, 0.7, 0.62, 0.88])

WebBrowser control (webBrowser1)

MenuItem control (mnuBack)

Figure 18-10

Set the Modifiers property of the WebBrowser control to Internal so that the control is accessible from other forms. Specifically, you want to set the content of the control from within Form1.