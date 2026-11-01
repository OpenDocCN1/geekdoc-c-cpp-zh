4. Once the project is initialized, add the following lines of code to the file displayed in the main window:

```
namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            // Output text to the screen.
            Console.WriteLine("The first app in Beginning Visual C# 2015!");
            Console.ReadKey();
        }
    }
}
```

5. Select the Debug -> Start Debugging menu item. After a few moments you should see the window shown in Figure 2-6.

![](bbox=[0.15, 0.56, 0.7, 0.64])

FIGURE 2-6

6. Press any key to exit the application (you might need to click on the console window to focus on it first). The display in Figure 2-6 appears only if the Visual C# Developer Settings are applied, as described earlier in this chapter. For example, with Visual Basic Developer Settings applied, an empty console window is displayed, and the application output appears in a window labeled Immediate. In this case, the Console.ReadKey() code also fails, and you see an error. If you experience this problem, the best solution for working through the examples in this book is to apply the Visual C# Developer Settings — that way, the results you see match the results shown here.

# How It Works

For now, I won't dissect the code used thus far because the focus here is on how to use the development tools to get code up and running. Clearly, Visual Studio does a lot of the work for you and makes the process of compiling and executing code simple. In fact, there are multiple ways to perform even these basic steps — for instance, you can create a new project by using the menu item mentioned earlier, by pressing Ctrl+Shift+N, or by clicking the corresponding icon in the toolbar.

Similarly, your code can be compiled and executed in several ways. The process you used in the example — selecting Debug -> Start Debugging — also has a keyboard shortcut (F5) and a toolbar icon. You can also run code without being in debugging mode using the Debug -> Start Without Debugging menu item (or by pressing Ctrl+F5), or compile your project without running it (with debugging on or off) using Build -> Build Solution or pressing F6. Note that you can execute a project without debugging or build a project using toolbar icons, although these icons don't appear on the toolbar by default. After you have compiled your code, you can also execute it simply by running the .exe file produced