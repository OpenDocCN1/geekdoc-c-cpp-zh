
![](img/0a07386735fd4e6427d20aa9bc165f5d_8_0.png)

*Figure 1: Extensions and Updates Menu Item*

This will open the **Extensions and Updates** window (Figure 2), from which you can search the Visual Studio Gallery. Incidentally, you are also able to include Code Contracts in your project via NuGet (more on that later).

In the search box to the right of the screen, enter **Code Contracts** and be sure to have the **Online** section selected in the tree view to the left. When your search results are returned, Code Contracts should be one of the top results. From here it is easy to install Code Contracts. Simply click the **Download** button, which will download an .msi installer that you can run to install Code Contracts.

![](img/0a07386735fd4e6427d20aa9bc165f5d_9_0.png)

## NuGet

The NuGet package manager can also be used to download and include Code Contracts in your solution. You can use the NuGet Package Manager (Figure 3) to search for Code Contracts, or you can use the Package Manager Console from the Tools > NuGet Package Manager option to run the following command to install Code Contracts.

```powershell
PM> Install-Package CodeContracts
```

You will also find a portable version (for use with Windows Mobile applications) of the Code Contracts package on NuGet. It doesn’t really matter which method you use to install Code Contracts; it’s just a matter which method you prefer.

![](img/0a07386735fd4e6427d20aa9bc165f5d_10_0.png)

*Figure 3: NuGet Package Manager*

## Visual Studio integration

You will need to restart Visual Studio for the Code Contracts item in the Properties page to become visible. The Code Contracts integration can be found by right-clicking on your project and selecting **Properties** from the context menu. You can also find the Code Contracts integration by selecting **Project** from the Visual Studio toolbar (be sure that you have selected your project in the Solution Explorer), and clicking the *ProjectName Properties* menu item (Figure 4).

I have called my Visual Studio project **CodeContractsDemo**, so the item in the **Projects** menu in Visual Studio will be called **CodeContractsDemo Properties**. The familiar Property page opens for your project, and at the bottom of the list on the left of the Property page you will see a new property pane called **Code Contracts**.

Clicking on this will display a smorgasbord of settings for you to select. Don't let the number of settings intimidate you; we will go through these in the next section. Only know that many of the settings are defaulted, and you can leave them that way should you wish to.

![](img/0a07386735fd4e6427d20aa9bc165f5d_11_0.png)

*Figure 4: Project Properties*

## Code Contracts property page

The Code Contracts properties will expose many options and settings to you initially. The properties under Code Contracts are separated into three groups: Runtime Checking, Static Checking, and Contract Reference Assembly.

Enable Code Contracts by selecting either **Perform Runtime Contract Checking** or **Perform Static Contract Checking**.

At minimum, you need to ensure that one of these options is selected in order to enable Code Contracts in your project. Without selecting either of these options, Code Contracts will not be enabled in your project, and you will not be able to benefit from the value they add to your system.

Runtime Contract Checking, as the name suggests, will work its magic during run-time. Static Contract Checking, however, is a different animal altogether. It lets Code Contracts analyze your code while you’re typing code or building your project. This is where Code Contracts become interesting and add the most value for me.

![](img/0a07386735fd4e6427d20aa9bc165f5d_12_0.png)

*Figure 5: Code Contracts Property Page*

## Static checking

If you enable static checking, it is advisable to keep the **Check in background** option selected in the Properties page. This is because analysis can take some time to perform. Another advisable option is to select the parallel build option in Visual Studio. From the **Tools** menu in Visual Studio, select **Options**. In the tree-view on the left of the Options screen (Figure 6), expand the **Projects and Solutions** node. You will notice a node called **Build and Run**. Select that, and you will see the option to enable parallel builds.

Any value greater than **1** will enable the parallel builds option in Visual Studio. The default value on my machine is **8**. Entering the value **1** in this text box will effectively switch off parallel builds in Visual Studio. By enabling parallel builds in Visual Studio, you enable Code Contracts to analyze several projects in parallel. According to RiSE, the Visual Studio extension is thread-safe. There are many other options available in the Code Contracts property page, but you can now start to use Code Contracts without having to configure these settings any further.

![](img/0a07386735fd4e6427d20aa9bc165f5d_13_0.png)

Figure 6: Visual Studio Parallel Builds Option

You will notice that Visual Studio 2015 suggests a few corrections. In Figure 7, you see that the **using** statement is the first suggestion, and is the fix we need to apply in this instance.

## Visual Studio 2015 light bulbs

This productivity feature is new in Visual Studio 2015. Light bulbs appear automatically in the Visual Studio editor and provide error-fixing and refactoring suggestions to the developer on the current line of code being typed. Light bulbs can also manually be invoked by pressing **Ctrl+Period** on a line of code to see a list of potential fixes.

## The Code Contract precondition

Consider the following code listing, which checks the value of the serial number being passed to the method. This method is used to add a serialized stock item to the inventory table of the new ERP system.

```csharp
public static class ERPIntegration
{
    public static void AddSerializedItem(string productCode, int
serialNumber, int qty)
    {
        Contract.Requires<SerialNumberException>
            (serialNumber >= 10000001, "Invalid Serial number");
    }
}

public class SerialNumberException : Exception
{
    public SerialNumberException()
    {
    }

    public SerialNumberException(string message)
        : base(message)
    {
    }

    public SerialNumberException(string message, Exception inner)
        : base(message, inner)
    {
    }
}
```

*Code Listing 2: Code Contract Precondition*

The Contract.Requires statement denotes a precondition. Preconditions are the first statements in the method body. In the previous code listing, the precondition checks the value of the serial number passed to the method and determines if it is a valid serial number.

Now let us take a closer look at the actual Code Contract. The Code Contract is put together as follows: Contract.Requires<TException>(bool condition, string errorMessage) where TException : Exception. The Boolean condition is validated, and if it fails, the Code Contract will throw an exception with the message provided. Note that I have added a custom exception to the contract called SerialNumberException. It is derived from the Exception class, but you can add any applicable exception here to suit your requirements.

The format of the Code Contract in the preceding code listing is but one implementation. The following list illustrates the valid syntax for the Code Contract preconditions:

- Contract.Requires(bool condition)
- Contract.Requires(bool condition, string errorMessage)
- Contract.Requires<TException>(bool condition)
- Contract.Requires<TException>(bool condition, string errorMessage)

Personally, I prefer the combination of a specified exception class and the user-defined error message thrown if the condition expressed in the Code Contract fails. This provides the developer with a very powerful mechanism to ensure that the values passed to the method are valid. It also frees the developer from having to defensively code for every eventuality that might break the system. Knowing that the method under contract will always answer to the predetermined rules you specified gives you more peace of mind as a developer.

## The Code Contract precondition in action

To illustrate the failure of the precondition defined in the Code Contract, I hard-coded an invalid serial number in the method call. Being a console application, the call to the method is wrapped in a try/catch statement that outputs the error to the console. Consider the following code listing.

```csharp
static void Main(string[] args)
{
    try
    {
        ERPIntegration.AddSerializedItem("BC32WL", 70012, 1);
    }
    catch (Exception ex)
    {
        Console.Write(ex.Message);
        Console.ReadLine();
    }
}
```

Code Listing 3: The Code Contract Precondition in Action
