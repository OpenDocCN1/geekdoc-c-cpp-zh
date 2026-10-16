current date and time.

The sample applications use AppSupport to fill a label with a string containing the current date. To use the examples, first load and build AppSupport. Then, in the ClientWPF project, set a reference to the newly built AppSupport.dll.

Here is the code for the AppSupport assembly:

```
using System;
namespace AppSupport
{
    public class DateService
    {
        public string GetLongDateInfoString() =>
            $"Today's date is {DateTime.Today:D}";

        public string GetShortDateInfoString() =>
            $"Today's date is {DateTime.Today:d}";
    }
}
```

This simple assembly suffices to demonstrate the deployment options available to you.

# xcopy Deployment

xcopy deployment is a term used for the process of copying a set of files to a folder on the target machine and then executing the application on the client. The term comes from the DOS command xcopy.exe. Regardless of the number of assemblies, if the files are copied into the same folder, the application will execute—rendering the task of editing the configuration settings or registry obsolete.

To see how an xcopy deployment works, execute the following steps:

+   1. Open the ClientWPF solution (ClientWPF.sln) that is part of the sample download file.
+   2. Change the target to Release and do a full compile.
+   3. Use the File Explorer to navigate to the project folder \ClientWPF\bin\Release and double-click ClientWPF.exe to run the application.
+   4. Click the button to see the current date displayed in the two text boxes. This verifies that the application functions properly. Of course, this folder is where Visual Studio placed the output, so you would expect the application to work.
+   5. Create a new folder and call it ClientWPFTest. Copy just the two assemblies (AppSupport.dll and ClientWPFTest.exe) from the release folder to this new folder and then delete the release folder. Again, double-click the ClientWPF.exe file to verify that it’s working.

That’s all there is to it; xcopy deployment provides the capability to deploy a fully functional application simply by copying the assemblies to the target machine. Although the example used here is simple, you