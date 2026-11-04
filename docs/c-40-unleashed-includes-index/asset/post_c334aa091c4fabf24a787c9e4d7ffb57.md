
![](img/a16f85e62ce9bdc527f4b09dbfe26092_177_0.png)

FIGURE 3.46   The integrated WPF designer.

One key difference is in the functionality exposed by the designer. First of all, observe the zoom slider on the left, reflecting WPF's resolution-independence capabilities. A more substantial difference lies in the separation between the designer surface and the XAML view at the bottom. With XAML, no typical code generation is involved at design time. Instead, XAML truly describes the UI definition in all its glory.

Based on this architecture, it's possible to design different tools (such as Expression Blend) that allow refinement of the UI without having to churn out C# code. The integrated designer therefore provides only the essential UI definition capabilities, decoupling more-involved design tasks from Visual Studio by delegating those to the more-specialized Expression Blend tool for use by professional graphical designers.

Again, double-clicking the button control generates the template code for writing an event handler to respond to the user clicking it. Although the signature of the event handler method differs slightly, the idea is the same. Figure 3.47 shows the generated empty event handler for a WPF event.

Notice, though, there's still a call to InitializeComponent in the Window1 class's constructor. But didn't I just say there's no code generation involved in WPF? That's almost true, and the code generated here does not contain the UI definition by itself. Instead, it contains the plumbing required to load the XAML file at runtime, to build up the UI. At the same time, it contains fields for all the controls that were added to the user interface for you to be able to address them in code. This generated code lives in a partial class definition stored in a file with a .g.i.cs extension, which is illustrated in Figure 3.48. To see this generated code file, toggle the Show All Files option in Solution Explorer.

```csharp
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;

namespace MyFirstWpfApplication
{
    /// <summary>
    /// Interaction logic for Window1.xaml
    /// </summary>
    public partial class Window1 : Window
    {
        public Window1()
        {
            InitializeComponent();
        }

        private void button_Click(object sender, RoutedEventArgs e)
        {

        }
    }
}
```

**FIGURE 3.47**  Code skeleton for an event handler in WPF.

```csharp
internal System.Windows.Controls.TextBox textBox1;

#line default
#line hidden

private bool _contentLoaded;

/// <summary>
/// InitializeComponent
/// </summary>
[System.Diagnostics.DebuggerNonUserCodeAttribute()]
public void InitializeComponent() {
    if (_contentLoaded) {
        return;
    }
    _contentLoaded = true;
    System.Uri resourceLocator = new System.Uri("/MyFirstWpfApplication;component/Window1.xaml", System.UriKind.Relative);
#line 1 "..\..\..\Window1.xaml"
    System.Windows.Application.LoadComponent(this, resourceLocator);
#line default
#line hidden
}
```

**FIGURE 3.48**  Generated code for a WPF window definition.

Notice how the XAML file (which gets compiled into the application’s assembly in a binary format called BAML) is loaded through the generated code. From that point on, the XAML is used to instantiate the user interface definition, ready for it to be displayed by WPF’s rendering engine.

As an aside, you can actually create WPF applications without using XAML at all by creating instances of the window and control types yourself. In other words, there’s nothing secretive about XAML; it’s just a huge convenience not to have to go through the burden of defining objects by hand.

payment services, sending out notifications to the shipping facilities, and so on. Workflow provides the necessary services to maintain this stateful long-running operation, carrying out suspend and resume actions with state (de)hydration when required.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_180_0.png)

FIGURE 3.49   A simple sequential workflow.

## WPF STRIKES AGAIN

Not only is Visual Studio 2010 presented using WPF technology, the new workflow designer is too. This clearly illustrates the richness that WPF can provide. Actually, the workflow designer can be rehosted in custom applications, too.

## ASP.NET

Also introduced right from the inception of the .NET Framework is ASP.NET, the server-side web technology successor to classic Active Server Pages (ASP). Core differences between the old and the new worlds in web programming with ASP-based technologies include the following:

- Support for rich .NET languages, leveraging foundations of object-oriented programming, eliminating the use of server-side script as with VBScript in classic ASP.
- First-class notion of controls that wrap the HTML and script aspects of client-side execution.
- Related to control support is the use of an event-driven approach to control interactions with the user, hiding the complexities of HTTP postbacks or AJAX script to make callbacks to the server.
- Various aspects, such as login facilities, user profiles, website navigation, and so on, have been given built-in library support to eliminate the need for users to reinvent the wheel for well-understood tasks. An example is the membership provider taking care of safe password storage, providing login and password reset controls, and so on.
- Easy deployment due to the .NET's xcopy vision. For instance, when requiring a class library to be deployed to the server, there's no need to perform server-side registrations in the world of .NET.
- A rich declarative configuration system makes deployment of web applications easier, having settings stored in a file that's deployed with the rest of the application over any upload mechanism of choice.

From the Visual Studio point of view, ASP.NET has rich project support with a built-in designer and deployment facilities. Figure 3.50 shows ASP.NET's page designer.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_181_0.png)

FIGURE 3.50   ASP.NET's page designer.

By now, designers should start to look very familiar. This time around, the markup is stored in HTML, containing various ASP.NET controls with an asp: prefix. The runat attribute set to server reveals the server-side processing involved, turning those controls into browser-compatible markup:

```html
<asp:Button ID="Button1" runat="server" Text="Say Hello" />
```

Again, the Toolbox contains a wealth of usable controls available for web development, and the Properties window joins the party to assist in configuring the controls with respect to appearance, behavior, data binding, and more. The designer surface is put in Split mode, to show both the HTML and ASP.NET source, together with the Designer view. Both are kept in sync with regard to updates and selections.

The designer is quite powerful, actually. Take a look at the various menus and toolbars that have been added for formatting, tables, the use of Cascading Style Sheets (CSS), and more. This said, for more complex web design, another Expression family tool exists: Expression Web. In a similar way to WPF with Expression Blend, this tandem of tools facilitates collaboration between developers and designers.

Hooking up event handlers is easy once more (testified by Figure 3.51’s generated event handler code). What goes on behind the scenes is much more involved. Although you still write managed code, ASP.NET wires up event handlers through postback mechanisms at runtime. With the introduction of AJAX, various postback operations can be made asynchronous as well. By doing so, no whole page refreshes have to be triggered by postback operations, improving the user experience a lot.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_182_0.png)

```csharp
using System;
using System.Web.UI;
using System.Web.UI.WebControls;

public partial class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
    }

    protected void Button1_Click(object sender, EventArgs e)
    {
    }
}
```

**FIGURE 3.51**  Event handler code in ASP.NET.

To simplify testing ASP.NET applications, a built-in ASP.NET Development Server comes with Visual Studio 2010, eliminating the need to install Internet Information Services (IIS) on development machines. The Development Server serves two goals. One is to facilitate debugging, and the other is to provide the site configuration web interface. Figure 3.52 shows the Development Server being launched in response to starting a debugging session (by a press of F5, for example).

![](img/a16f85e62ce9bdc527f4b09dbfe26092_182_1.png)

**FIGURE 3.52**  The Development Server has started.

Debugging ASP.NET applications is as simple as debugging any regular kind of application, despite the more complex interactions that happen under the covers. In the latest releases
