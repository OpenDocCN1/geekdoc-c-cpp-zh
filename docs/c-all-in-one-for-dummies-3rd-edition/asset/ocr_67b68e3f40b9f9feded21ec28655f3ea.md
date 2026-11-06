![](bbox=[0.253, 0.135, 0.729, 0.456])

**Figure 3-3:** Change the compiler settings to meet your project needs.

**8. Change any required compiler settings and click Finish.**

The wizard creates the application for you. It then displays the Code::Blocks IDE with the project loaded. Note that the Static Library project includes some sample code to get you started. You could compile this library and test it now.

# ## Configuring the library project

The static library starts with a standard C file. To make this library work well with templates, you need to delete the C file, add a C++ file, and add a header file. The following steps describe how to perform this process:

+   1. **Right-click main.c in the Projects Tab of the Management window and choose Remove File From Project from the context menu that appears.**
+      Code::Blocks removes the file from the project tree.
+   
+   2. **Choose File»New»File.**
+      You see the New from Template dialog box shown in Figure 3-4.
+   
+   3. **Highlight the C/C++ Header icon and click Go.**
+      You see the Welcome page of the C/C++ Header wizard.
+   
+   4. **Click Next.**
+      The wizard asks you to provide the header configuration information (see Figure 3-5).