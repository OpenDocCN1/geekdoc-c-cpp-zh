```
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Classes2
{
    class MessageClass
    {
        public string FirstMessage()
        {
            return "This is the first message coming from the " +
                   "FirstMessage method of the MessageClass.";
        }
        public string SecondMessage()
        {
            return "This is the second message coming from the " +
                   "SecondMessage method of the MessageClass.";
        }
    }
}
```
```

Code 12.14 – MessageClass.cs file

10.Build and run the project. The Text of the Label will be changed according to the clicked Button. FirstMessage() or SecondMessage() method will be called which will display the first message or the second message on the Label:

![](bbox=[0.27, 0.76, 0.68, 0.9])

Figure 12.13. The first message is shown on the Label using the string returned from the FirstMessage() method