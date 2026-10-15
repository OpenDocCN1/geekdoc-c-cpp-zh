ThisDocument code should be the newly generated property value, as shown in Figure 25-9. The resulting code should look similar to the following:

```
Property Get CallVSTOAssembly() As VBAInterop.ThisDocument
    Set CallVSTOAssembly = GetManagedClass(Me)
End Property
```

![](bbox=[0.094, 0.183, 0.697, 0.489])

**FIGURE 25-9**

The code in this block shows the newly generated property that associates your VBA environment with the VSTO code you are creating. You can then proceed to the placeholder comment in the Document_New method where you initially entered a comment to maintain your macro’s existence. Within this method, on a new line, make a call to CallVSTOAssembly, and you’ll have IntelliSense for the list of available methods and properties.

There are a few additional steps in order to enable VBA to connect to VSTO, but for those who are already working with VBA these steps won’t be a significant challenge. After all, it is development experience and the ability to continue to leverage existing resources that really drive this interop feature. The fact that this feature is so natural for a VBA developer — who may want to leverage key new capabilities such as WCF, WF, or possibly even WPF-based graphics in Excel — means that you can expect to be able to leverage your existing VBA code for several more years. When you do “migrate,” the process is one that you control and execute in stages based on your requirements and decisions, not some overriding conversion process.

# CREATING A DOCUMENT TEMPLATE (WORD)

The previous section introduced you to creating a document template from the standpoint of interoperating with VBA; but unless you have an existing VBA application, in most cases you’ll just create a new, clean Word Document project. These projects focus on a specific document. They are self-contained in the sense that your changes only affect the user’s system when the user chooses to open a document that specifically includes your changes.

This is great, as it isolates your changes. When users open Word or Excel they don’t automatically load your customization. This way, your code won’t affect the overall performance of their system (not that most developers care about this). The model also means that customizations for Application A aren’t competing with Application B, which is in some ways a bigger challenge with add-ins.