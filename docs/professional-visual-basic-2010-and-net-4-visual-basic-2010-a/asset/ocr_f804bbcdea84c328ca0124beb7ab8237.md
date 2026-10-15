method has an attribute as part of its declaration. Each type of class member that is to be exposed gets an attribute matching the type of that method. Thus, for the New method, the type of the attribute is InteropFormInitializer. For this simple example, the parameterized New(ByVal label As String) simply changes the text associated with the label. Finally, although this class is defined in .NET syntax, COM and VB6 don’t allow parameterized New statements. Thus, when you reference this parameterized initializer, you’ll find that the method name is in fact Initialize.

Next, the code defines and exposes a public property. In this case, to help simplify the code, there isn’t a private member variable to hold the value; this provides an easy way for the code that creates this form to set and retrieve the value of the text box. Similarly, there is a method to allow the calling code to update the label shown on the form. Note that it has also been attributed; and after you update the label for demonstration purposes, it raises the custom event that is defined next.

That event, called CustomEvent, is defined with an attribute, but the event that is defined must also define the signature or definition of its handlers. In this case, the Delegate CustomEventSig handles a single parameter. This .NET code, as noted, provides a basic example of each of the primary types of Interop you’ll want to carry out. The next step is to generate your Interop methods.

One of the key differences between an InteropForms project and an Interop User Control project is this step. Only the InteropForms project requires the generation of custom COM wrappers. To do this, access the Tools menu and select Generate InteropForm Wrapper Classes. There is no user interface; instead, the generation process will create a new directory in your project containing the InteropForm1.wrapper.vb class, as shown in Figure B-3.

> For readers developing on Vista and Windows 7: Keep in mind that registry access requires elevated permissions. You need to start Visual Studio with the Run as Administrator option on your right-click context menu. If you don’t, then when you attempt to automatically register your newly built DLL as a COM component, you’ll get an error, which Visual Studio reflects as a Build Error.

![](bbox=[0.09, 0.56, 0.68, 0.91])

FIGURE B-3