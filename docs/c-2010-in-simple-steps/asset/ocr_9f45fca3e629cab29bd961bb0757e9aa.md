![](bbox=[0.255, 0.148, 0.725, 0.272])

**Fig.C#-5.7**

A new form named **SecondForm** is added to the **SampleApplication** application, as shown in Fig.C#-5.8:

![](bbox=[0.26, 0.321, 0.731, 0.451])

**Fig.C#-5.8**

In the same way, you can add more forms to your application.

# ## Setting the Startup Form in a Multiform Windows Forms Application

Whenever you open a multiform Windows Forms application, the **Form1** form appears as the default startup form; however, you can also set any other form as the startup form. In C#, you can set the startup form in the **Program.cs** file.

Perform the following steps in the **SampleApplication** application to set the **SecondForm** as the startup form in a multiform Windows Forms application:

+   1. **Double-click** the **Program.cs** file in Solution Explorer. The Code Editor appears with the code, as shown in Listing 5.1:

**Listing 5.1: Showing the Code of Program.cs File**

```
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Windows.Forms;

namespace SampleApplication
{
    static class Program
    {
        /// <summary>
        /// The main entry point for the application.
        /// </summary>
        [STAThread]
```
```