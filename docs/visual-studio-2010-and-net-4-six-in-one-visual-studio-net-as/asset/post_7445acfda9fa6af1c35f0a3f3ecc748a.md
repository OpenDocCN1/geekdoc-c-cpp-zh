
All the items you see in the middle pane of the New Project dialog templates that cover an entire project, including the project file (with the properties set up), all source files (including resources, content files, associated document files, and so on), and the references used by the project.

The project files templates also contain some other metadata that is used by the IDE to display information about the project. For example, a short description of the project is shown on the pane of the dialog. Data also includes information to categorize templates in the UI. Templates for example, they can disable the Browse button.

When you create a project instance from the selected project template, the template system copies all files from the template to a specified location. In addition to the copy operation:

- The template system can replace strings in the filenames and in the content of them. For example, the project name can replace the project file, and also the default name specifications in the source code files.
- A wizard can be started that collects some information about the project and uses this information when generating project artifacts.

Let's say that you create a new WPF application with the name of MyWpfApp. Figure 4-3 shows the template system that enables you to start with the project.

The project template contains all the files shown in Figure 4-3. As you see, the project filename has been changed to MyWpfApp. If you open the App.xml.cs file, you would see that the root namespace has also been renamed to MyWpfApp.

## Item Templates

When you create a project based on a specific template, you can also add new items to this project, and you would like to start with a well-defined item skeleton instead of an empty code file. This is where the items come into the picture.

During your everyday activities, you generally work with a few stereotypes of project items such as forms, entity classes, service and controller types, database scripts, and so on. Visual Studio provides a great number of item templates you can add to your project with the Add New Item dialog. Figure 4-4 shows the items you can choose when working with WPF application.

![](img/b5597c749e848b27b0d305153ae16106_110_0.png)

FIGURE 4-3: The new project in Solution Explorer

![](img/b5597c749e848b27b0d305153ae16106_111_0.png)

**FIGURE 4-4:** The Add New Item dialog

This dialog is very similar to the New Project dialog, and so are the mechanisms behind the UI. The template system works approximately the same way for item templates as project templates — all item templates files are copied to the project folder. Replacements and wizards are also supported for item templates.

Item templates provide a feature to enable you to add assembly references to the project hosting the item. In the template definition, an item can enlist referenced assemblies that the item is about to use for successful compilation. When the item is added to the project, all referenced assemblies that are not yet assigned to the project are also added.

Items and files are separate concepts. Although most items hold a single file, few of them are composed of several files — such as forms and resources that may contain two (or three) dependent files as a hierarchy within the Solution Explorer. An item template is definitely not a file template, so each file composing an item can be (and should) be added to the item template.

An item template may include more items to add to your project. For example, you may create an item for an entity that adds two files using partial class declaration with the intention that the user should customize only one of them. These are separate items (that is, you can handle them separately), and, in the project, there is no information to indicate that they were added in a single step.

## CREATING TEMPLATES

By now, you are familiar with the idea of project and item templates. Let’s have a look at how these concepts work in practice. In this, you create a simple project template and a related item template. The activities here can be repeated for your own project and item templates.

The creation process starts with actually implementing the application, library, page, form, class, or whatever artifacts that you intend to base your template. When these artifacts are ready, you can use the Export Template Wizard in Visual Studio to physically create the template definition, and integrate it with the IDE. You can also add customization points to the template.

## Creating a Simple Project Template

To demonstrate the steps of template creation, let's build a console application that receives commands from the window and executes them. Of course, the application will be very simple and not robust, this sample focuses on template development.

## Creating the Startup Project

Create a new C# project with the File -> New -> Project and select the Console Application from the Windows project category. Name this application ConsoleBase and click OK. Visual Studio creates a new application with Program.cs and AssemblyInfo.cs files. (You can display this file when extending the Properties folder.) This application does not run any code by default. So, let's change the Program class to implement a very simple console application's logic, as shown in Listing 4-1.

- LISTING 4-1: Program.cs

![](img/b5597c749e848b27b0d305153ae16106_112_0.png)

```
using System;

namespace ConsoleBase
{
    class Program
    {
        const string PromptText = "# >";
        const string QuitCommand = "quit";

        static void Main(string[] args)
        {
            DisplayWelcomeMessage();
            Console.Write(PromptText);
            string command;
            string[] pars;
            while (String.Compare(command = ReadCommand(out pars)),
                QuitCommand, true) != 0)
            {
                ProcessCommand(command, pars);
                Console.Write(PromptText);
            }
        }

        static void DisplayWelcomeMessage()
        {
            Console.WriteLine("Welcome to the BaseConsole application!");
            Console.WriteLine();
        }
    }
}
```

# LISTING 4-1 (continued)

```
static string ReadCommand(out string pars)
{
    var CommandLine = Console.ReadLine().Trim();
    var command = commandLine;
    pars = string.Empty;
    var pos = CommandLine.IndexOf(' ');
    if (pos > 0)
    {
        command = CommandLine.Substring(0, pos);
        pars = CommandLine.Substring(pos).Trim();
    }
    return command;
}

static void ProcessCommand(string command, string pars)
{
    Console.WriteLine("*{0}(\{1}) processed", command, pars);
}
```

Code file [Program.cs] available for download at Wrox.

The class is very simple. It displays welcome text and loops with processing commands typed by the user unless a "quit" command arrives, at which time it terminates. When you build and start it without debugging, you can see how it works. Figure 4-5 shows some output.

![](img/b5597c749e848b27b0d305153ae16106_113_0.png)

FIGURE 4-5: Sample output from BaseConsole

You are now ready to create a project from this application. Go to the File menu and select the Export Template. A new dialog, the Export Template Wizard, pops up on the screen. This wizard has a few pages, the first of which enables you to select the template type you intend to export, as shown in Figure 4-6.

![](img/b5597c749e848b27b0d305153ae16106_114_0.png)

Figure 4-6: The Choose Template Type page

You want to export BaseConsole as a project template, so select that option. At the bottom of the page, you can select the project the template is based on. This list shows projects in the current solution.

Click the Next button, and the wizard moves you to the Select Template Options page, where you can specify a few attributes. Fill these options as shown in Figure 4-7.

![](img/b5597c749e848b27b0d305153ae16106_114_1.png)

Figure 4-7: The Select Template Options page
