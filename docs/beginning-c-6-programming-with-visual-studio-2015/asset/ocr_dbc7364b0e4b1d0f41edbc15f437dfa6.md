```
```csharp
using System.Linq;
using System.Text;
using static System.Console;
using System.Threading.Text;
```
```

3. Add the following code to the Main() method in Program.cs:

```
```csharp
static void Main(string[] args)
{
    string[] names = { "Alonso", "Zheng", "Smith", "Jones", "Smythe",
    "Small", "Ruiz", "Hsieh", "Jorgenson", "Ilyich", "Singh", "Samba", "Fatimah" };
    var queryResults =
        from n in names
        where n.StartsWith("S")
        select n;
    WriteLine("Names beginning with S:");
    foreach (var item in queryResults) {
        WriteLine(item);
    }
    Write("Program finished, press Enter/Return to continue:");
    ReadLine();
}
```
```

4. Compile and execute the program (you can just press F5 for Start Debugging). You will see the names in the list beginning with S in the order they were declared in the array, as shown here:

```
```
Names beginning with S:
Smith
Smythe
Small
Singh
Samba
Program finished, press Enter/Return to continue:
```
```

Simply press Enter/Return to finish the program and make the console screen disappear. If you used Ctrl+F5 (Start Without Debugging), you may need to press Enter/Return twice. That finishes the program run.

# How It Works

The first step is to reference the System.Linq namespace, which is done automatically by Visual Studio 2015 when you create a project:

```
```csharp
using System.Linq;
```
```

All the underlying base system support classes for LINQ reside in the System.Linq namespace. If you create a C# source file outside of Visual Studio 2015 or edit a project created from a previous version, you may have to add the using System.Linq directive manually.

The next step is to create some data, which is done in this example by declaring and initializing the array of names:

```
```csharp
string[] names = { "Alonso", "Zheng", "Smith", "Jones", "Smythe", "Small",
"Ruiz", "Hsieh", "Jorgenson", "Ilyich", "Singh", "Samba", "Fatimah" };
```
```