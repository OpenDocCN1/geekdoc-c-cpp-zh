# **Note**

A client machine does not need to have the DLLs that implement the server objects installed in order to create instances of the objects, nor does it need MTS installed. The only things the client requires are the class ID GUID (CLSID) and the interface GUIDs (IIDs) in the registry. The client also needs the type library for the server so that the type library marshaler can marshal the interfaces between the two machines when the server uses type library marshaling or the proxy/stub DLL when the server requires standard marshaling. The setup program generated from exporting the package takes care of installing the type library, or the proxy/stub DLL, and adding the necessary keys to the registry. It creates a subdirectory called Remote Applications under the Program Files directory and installs the type library or proxy/stub DLL there. However, in the case in which the server has the type library embedded as a resource in the DLL, make sure to also add the type library file (TLB) to the package as a separate DLL. Otherwise, MTS will add the server files to the client setup instead of simply adding the type library file.

# ## Exporting a Package

When you are ready to move your application to a production server, you will want to export your package.

To export a package, do the following:

+   1. In MTS Explorer, right-click the package you want to export, and select Export. The Export Package dialog box appears.
+   2. Type the exact path and name for the package. If you want to export the user IDs for each role, select the Save Windows NT User IDs Associated With Roles check box. This check box refers only to the users in the roles. If you do not select this check box, the role information will still be exported, but the actual user IDs within the role will not be included. This is normally what you want to do when moving from development to deployment. Click Export.
+   3. If this is not the first time you're exporting a package to the same location, the Overwrite Files dialog box will prompt you to overwrite the old package and DLL. Click OK.
+   4. The Export Package dialog box closes. When the export is complete, MTS Explorer reappears with a message box telling you that the package was exported successfully. Click OK.