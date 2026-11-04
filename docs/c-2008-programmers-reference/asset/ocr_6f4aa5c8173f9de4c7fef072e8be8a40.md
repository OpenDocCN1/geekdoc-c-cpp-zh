# Part I: C# Fundamentals

Switch to the code-behind of the default Form1 and code the following statements:

```
```csharp
namespace WindowsApp_Util
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            CallUtil();
        }

        private void CallUtil()
        {
            MathUtil.Utils util = new MathUtil.Utils();
            MessageBox.Show(util.Fibonacci(7).ToString());
        }
    }
}
```
```

Set a breakpoint at the CallMathUtil() method (see Figure 15-8).

![](bbox=[0.27, 0.68, 0.72, 0.84])

Right-click on the WindowsApp_Util project name in Solution Explorer, and select Start as Startup Project. Press F5 to debug the application. When the application stops at the breakpoint, view the modules loaded into memory by selecting Debug ⇨ Windows ⇨ Modules (see Figure 15-9).