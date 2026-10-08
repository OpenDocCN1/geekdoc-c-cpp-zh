+   6. Add additional “properties” to the contact class and output them in Console.WriteLine statements.

+   7. Run the application again by pressing Ctrl+F5 and observe that the output changes to show the additional properties added.

# # Interoperating with COM

Although the .NET Framework has always enabled you to interoperate with COM, particularly with the Office COM APIs, the DLR simplifies the code you have to write considerably. Because many COM methods return types as object, the dynamic type enables you to easily treat them as dynamic objects instead.

To interoperate with COM APIs, you make use of a Primary Interop Assembly (PIA), which forms a bridge between the unmanaged COM API and the managed .NET application. To do this, you add a reference to the PIA in your Visual Studio project, allowing your application access to the types defined. When the reference has been added, you can choose to embed only those types actually used by your application.

![](bbox=[0.81, 0.5, 0.94, 0.53])

**Embedded Primary Interop Assemblies**

Because each PIA must contain a managed equivalent for every type, interface, enumeration, and so on defined in the COM API, some, such as the Office PIAs, can be quite large.

Only embedding the interop types used by your application can help reduce the size of your deployment and does not require the PIAs to be deployed at all. This also allows you to avoid a lot of the complexity of working with COM APIs by treating the object occurrences in the COM signatures as dynamic instead.

The code in Listing 21.7 shows a simple example of how to open a Microsoft Word document using COM interop.

# LISTING 21.7 COM Interop Without Dynamic Types

```
public static Main(string[] args)
{
    object missing = System.Reflection.Missing.Value;
    object readOnly = false;
    object isVisible = true;
    object fileName = "SampleDocument.docx";

    Microsoft.Office.Interop.Word.ApplicationClass wordApp =
        new Microsoft.Office.Interop.Word.ApplicationClass();
    wordApp.Visible = true;
```