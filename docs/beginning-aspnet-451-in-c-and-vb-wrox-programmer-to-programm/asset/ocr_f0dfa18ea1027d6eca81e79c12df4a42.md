# THE BASICS OF DEBUGGING

Debugging is the process of finding and fixing bugs in your code. Although that may sound easy, it often isn’t. Some bugs are very obvious and easy to spot and thus easy to fix. Others are much harder to find and require knowledge about the execution environment of your program. The debugging tools that ship with Visual Studio help you understand this execution environment by giving you direct access to the inner workings of your program or web page.

Debugging with VS is like snapping your fingers to stop the time. When you do that, everything halts, except for you, so you can walk around in your code, investigate variables, look into objects, try out methods, and even execute new code. To tell VS where to halt, you need to set one or more breakpoints in your code. When the code under the breakpoint is about to be executed, VS stops the execution of the application (usually a web page, a user control, or code in the App_Code folder) and then puts focus back on VS so you can diagnose the code and its environment.

You set a breakpoint by pressing F9 on the line of code where you want execution to halt. Instead of the F9 shortcut key, you can also click the margin of the code, where the big dot appears in Figure 18-6, or you can choose Debug ⇨ Toggle Breakpoint from the main menu. Pressing F9, clicking the same spot in the margin, or choosing the menu item again toggles the presence of the breakpoint. To clear all breakpoints in your entire website, press Ctrl+Shift+F9.

To give you an idea of how debugging works, and what it can do to help you, the following exercise shows you the basic operations of debugging. Later parts of this chapter give you a detailed look at the numerous debugging tools and windows that ship with VS.

# TRY IT OUT Debugging Your Application

In this Try It Out, you debug the Calculator page you created in a previous chapter. If you don’t have the file, refer to Chapter 5 or download the code for this chapter from www.wrox.com. The debugging exercises in this chapter assume you are using Internet Explorer as your browser. If you are using a different default browser, such as Firefox or Opera, the debugging experience will be largely the same, although you may find that VS does not always get the focus automatically while breaking into your code.

+   1. Open the CalculatorDemo.aspx page from the Demos folder and switch to Code Behind.
2. Click the first line of code in the CalculateButton_Click handler that checks the length of the text in the two TextBox controls. Then press F9 to set a breakpoint. The line gets highlighted, as shown in Figure 18-6, and a colored dot appears in the margin of the Document Window.

```
protected void CalculateButton_Click(object sender, EventArgs e)
{
    if (ValueBox1.Text.Length > 0 && ValueBox2.Text.Length > 0)
    {
        double result = 0;
        double value1 = Convert.ToDouble(ValueBox1.Text);
        double value2 = Convert.ToDouble(ValueBox2.Text);
    }
```

FIGURE 18-6