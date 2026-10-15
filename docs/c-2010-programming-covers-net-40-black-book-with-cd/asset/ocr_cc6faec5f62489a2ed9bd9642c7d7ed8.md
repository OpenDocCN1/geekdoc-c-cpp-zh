6. Right-click the class name, Service1, in the Service1.cs file and select the Refactor→Rename option from the context menu. The Rename dialog box opens (Figure 20.2).

7. Enter a new name for the service in the New name text box. In our case, the service name is MyService, as shown in Figure 20.2:

![](bbox=[0.225, 0.133, 0.74, 0.39])

Figure 20.2: Renaming the Service Name

8. Click the OK button in the Rename dialog box to rename the service name. The Preview Changes - Rename dialog box appears that displays a preview of changes in code after you rename the service, as shown in Figure 20.3:

![](bbox=[0.26, 0.463, 0.705, 0.72])

Figure 20.3: Previewing the Code Changes after Renaming the Service

9. Click the Apply button in the Preview Changes - Rename dialog box to confirm the renaming of the service. After creating a Windows service project, let's learn how to write event entries to the event log.

# Writing to an Event Log

You can write to an event log with the help of the Windows service application by using the WriteEntry method of the EventLog class. Let's add the WriteEntry() method of the EventLog class in the Service1.cs code-behind file of the MyWindowsService application. Listing 20.1 shows the code of the Service1.cs file:

Listing 20.1: Showing the Code of the Service1.cs File

```
using System;
using System.Collections.Generic;
```