![](bbox=[0.28, 0.16, 0.85, 0.66])

Figure 3-5:
The Service Configuration Editor.

Using the Service Configuration Editor for adding a service endpoint seems more complex than it ought to be. Just follow these steps:

+   1. **Open the Web.config of your project by clicking File... Open and navigate to your Web.config.**
+   2. **Select File->Add New then click Create a New Service.**
+   3. **Click Browse and find the compiled DLL of your project.**
+      It should be in the Bin folder, and named `SHARPService.dll` if you used my naming.
+   4. **Double-click on the DLL, and the services that are represented show up. As shown in Figure 3-6, click the Registration service. Click Open, and then Next.**
+   5. **Confirm the service contract.**
+      (See, I told you it would be useful later!)
+   6. **Click Next.**
+      In the Binding Configuration window, you'll see what I mean about the number of options. Select the Existing Binding Configuration radio button and check out the drop-down list. The items in that list are covered in the sidebar, "Using different endpoints." For now, accept the default.
+   7. **Click Next.**