# Making the Shared Assembly Visible in Visual Studio

By default, adding a shared assembly into the GAC does not make it appear automatically in Visual Studio’s Add Reference dialog. You need to add a registry key for that to happen. Here’s how to handle that.

First, launch the registry editor by typing regedit in the Run command box.

> > **If you are using Windows Vista, make sure to run regedit as Administrator.**

Navigate to the HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\AssemblyFolders key. Right-click on the AssemblyFolders key and select New > Key (see Figure 15-39).

![](bbox=[0.336, 0.298, 0.631, 0.503])

Name the new key Base64Codec. Double-click on the key’s (Default) value, and enter the full path of the shared assembly (for example, C:\Documents and Settings\Wei-Meng Lee\My Documents\Visual Studio 2008\Projects\Base64Codec\bin\Debug; see Figure 15-40).

![](bbox=[0.336, 0.595, 0.831, 0.835])

Then restart Visual Studio 2008, and the assembly should appear in the Add Reference dialog.