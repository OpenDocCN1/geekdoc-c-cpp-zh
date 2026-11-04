```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Linq;
using System.Text;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;

namespace NewServerControl
{
    [DefaultProperty("Text")]
    [ToolboxData("<{0}:ServerControl runat=server></{0}:ServerControl>")]
    public class ServerControl : WebControl
    {
        [Bindable(true)]
        [Category("Appearance")]
        [DefaultValue("")]
        [Localizable(true)]
        public string Text
        {
            get
            {
                String s = (String)ViewState["Text"];
                return (s == null) ? ("*" + this.ID + "*") : s;
            }
            set
            {
                ViewState["Text"] = value;
            }
        }

        protected override void RenderContents(HtmlTextWriter output)
        {
            output.Write(Text);
        }
    }
```

One property and one method appear in the default configuration. A server control is basically just text output to the screen. It causes markup, just like a Label control emits a set of <span> tags. If you want this control to emit a set of <div> tags, you just change the property get statement.

For more information about making good controls, search for Server Control in MSDN. There are a number of good articles, and anything from ASP.NET 2.0 or later works just fine.