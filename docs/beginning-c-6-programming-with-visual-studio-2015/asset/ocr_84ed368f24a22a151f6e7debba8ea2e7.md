7. Click OK to add the service reference.

8. Modify the code in Program.cs in the Ch22Ex01Client application as follows:

```
```csharp
using Ch22Ex01Client.ServiceReference1;
using static System.Console;

namespace Ch22Ex01Client
{
    class Program
    {
        static void Main(string[] args)
        {
            Title = "Ch22Ex01Client";
            string numericInput = null;
            int intParam;
            do
            {
                WriteLine("Enter an integer and press enter to call the WCF service.");
                numericInput = ReadLine();
            }
            while (!int.TryParse(numericInput, out intParam));
            ServiceClient client = new ServiceClient();
            WriteLine(client.GetData(intParam));
            WriteLine("Press a key to exit.");
            ReadKey();
        }
    }
}
```
```

9. Right-click the Ch22Ex01Client project in the Solution Explorer and select Set as StartUp Project.

10. Run the application. Enter a number in the console application window and press Enter. The result is shown in Figure 22-1.

![](bbox=[0.22, 0.72, 0.58, 0.82])

FIGURE 22-1

11. Exit the application, right-click the Service1.svc file in the Ch22Ex01 project in the Solution Explorer, and click View in Browser.

12. Review the information in the window.

13. Click the link at the top of the web page for the service to view the WSDL. Don’t panic — you don’t need to understand all the stuff in the WSDL file!

# How It Works

In this example you created a simple web server-hosted WCF service and console application client. You used the default Visual Studio template for a WCF service project, which meant that you didn’t have to add any code. Instead, you used one of the operations defined in this default template,