# Adding Custom Controls 703

This is a boring example, but you can see how this can be used to collect commonly used fields for reuse in an application. Order details, addresses, and map coordinates, among other types of information, all are usually grouped together and make great user controls. In a travel application I recently worked on, the start city and the end city and date became user controls. It's a great way to solve simple reuse problems.

# Adding Custom Controls

Beyond the scope of a user control is a control that — perhaps no one has thought of before. Maybe your company makes a device with a pressure gauge that you need to replicate in code. Or you need to display a unique set of patient statistics on a monitor, or demonstrate the running of some data engine.

Those kinds of controls call for the next level: custom controls, sometimes called server controls. A custom control is a web control built using the tools that Microsoft uses to build the controls that you have used throughout this chapter.

I won't fool you — building a server control is nontrivial. If one started, you need a new project, not just a new file. The project type is a Server Control project, and it gives us a battery of code to start with, like this:

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Linq;
using System.Text;
using System.Web;
using System.Web.UI;
using System.Web.Controls;
```

```
namespace ServerControl
{
    [Property("Text")
    [ToolData<{0}>ServerControl runat="server">{0}</ServerControl>]
    public class ServerControl : WebControl
    {
        [Bindable(true)]
        [Category("Appearance")
        [DefaultValue("")]
        [Localizable(true)]
        public string Text
        {
            get
            {
                String s = {(String)ViewState["Text"];
                return (s == null) ? "*" + this.ID + "*" : s;
            }
        }
    }
}

```

| Book VI
Chapter 3 |
Controlling Your
Development
Experience |