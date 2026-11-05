
When the console application is run, the exception is thrown and displayed in the console window. When using a Code Contract that has a custom exception, such as the one shown in Code Listing 2, you must set the Code Contracts Assembly Mode property to **Standard Contract Requires**.

![](img/0a07386735fd4e6427d20aa9bc165f5d_17_0.png)

*Figure 8: Precondition Failed*

This preceding example is a rather simple way to illustrate the power of Code Contracts. In a production system, however, one would obviously not have hard-coded values in the method call. The possibility that these values would come from a database or from user input is very high. As we all know, all input (user or data store) is something beyond our control, and we should treat it as such. Code Contracts mitigate the negative effects of bad data.

While the preceding example is functional, I want more from my Code Contract. I do not want to run my application and then realize that there are sections of code that cause my contracts to fail. Personally, I would like to see any failures at the moment I build my project. This project is small enough, so I can be a bit cavalier with the Code Contract properties as specified in the Project Properties window.

## Fail build on warnings

Return to the Code Contracts property page, and if you haven't already done so, enable **Perform Static Contract Checking**. Next, you need to clear the **Check in background** option. Then you will see that the **Fail build on warnings** option is enabled. Select this option.

![](img/0a07386735fd4e6427d20aa9bc165f5d_17_1.png)

*Figure 9: Enable Fail Build on Warnings*

Go ahead and build your project. Static Contract Checking kicks in immediately, and because your Code Contract does not pass, your build will fail, as shown in Figure 10. There is, however, a problem. Your Error List is empty even though your build failed. Because we only have a single Code Contract, we know where to look. This, however, isn't feasible when we have several code contracts.

![](img/0a07386735fd4e6427d20aa9bc165f5d_18_0.png)

*Figure 10: Visual Studio 2015 Build Failed*

So what went wrong? To find the issue causing the build failure, head over to the Output window. If you don't see the Output window, press Ctrl+W, O to bring it into view. You will then see the results of the build and the Code Contract that failed.

![](img/0a07386735fd4e6427d20aa9bc165f5d_18_1.png)

*Figure 11: Visual Studio Output Window*

With the current version 1.9.10714.2 of Code Contracts, the build errors not being output to the Error List has been identified as a bug in the release for Visual Studio 2015. This bug has been fixed and will be included in the next release of Code Contracts. For more information on this issue relating to Code Contracts for Visual Studio 2015, have a look at pull request 166 and issue 137 on GitHub. If you want to view all the open issues regarding Code Contracts, have a look at the Issues on the Code Contracts GitHub page.

Code Contracts is the result of a handful of dedicated individuals who continually work to improve the current version. It's up to users like us to report issues we come across, and in doing so, build a healthy community of influencers and a more stable product. Lastly, since it's open source, you can contribute to Code Contracts and be a part of this incredible Visual Studio extension.

## The Code Contract postcondition

The Code Contract postcondition is the method under contract's way of guaranteeing to the calling code that it will return a specific result if all the preconditions are met. Let us go back to the analogy of a bank and a loan for which a contract is drawn up. The bank ensures that the loan will have a fixed interest rate, but only if the repayments are made on time and for the amount due. The payments made by you can be equated to the preconditions of the Code Contract. The fact that the bank ensures a fixed interest rate can be equated to the postcondition.

It is therefore no surprise that the syntax of Code Contract postconditions use the Ensures method. Another interesting point to take note of is that while the postcondition validates the result of the method under contract, it must appear immediately after the preconditions in the method. Consider the following code sample:

```csharp
public static Warehouse AddSerializedItem(string productCode, int serialNumber, int qty)
{
    Contract.Requires<SerialNumberException>
        (serialNumber >= 10000001, "Invalid Serial number");
    Contract.Ensures(Contract.Result<Warehouse>() != null);

    ProductCode = productCode;
    SerialNumber = serialNumber;
    Quantity = qty;

    return CreateItem();
}
```

*Code Listing 4: Contract Postcondition*

As you can see from the previous code listing, I have expanded our method slightly. I have added the postcondition that tells the calling code that the return value of this method will be of type Warehouse and that it will not be null. The calling code therefore does not need to check if the object being returned to it is valid or not. The contract specifies that it will return a **Warehouse** object to it.

```csharp
Contract.Ensures(Contract.Result<Warehouse>() != null);
```

*Code Listing 5: The Code Contract Ensures a Result*

In the real-world example, this basically means that the created stock item will be issued to a specific warehouse based on a certain condition (the product code). The product code identifies the product as a fast mover, raw material, finished good, etc., and has to be issued to the correct warehouse upon creation. Our **AddSerializedItem** method under contract tells the calling code that it ensures the result of this warehouse issue will be stored in the **Warehouse** object. If anything goes wrong, the product code will be issued to a default warehouse. Users of the ERP system can inspect items stored in the default warehouse and manually issue the product codes to the correct warehouse at a later stage.

![](img/0a07386735fd4e6427d20aa9bc165f5d_20_0.png)

*Figure 12: Code Contract Postcondition Result*

I have included the **CreateItem()** method's code in the following code listing. While this code sample is shown merely to explain a concept, the logic is sound. The **switch** statement will have a fixed set of cases it examines, as shown in Code Listing 6. It would not, however, have hard-coded values for the **Warehouse** object it returns. These would be read from a database or other object as the code interacts with the ERP to create the product code entry and issue it to a warehouse. What the code logic does ensure is that the method will always return a **Warehouse** object, and that object will always be a valid warehouse in the system.

```csharp
private static Warehouse CreateItem()
{
    // Add Stocked Item code goes here
    Warehouse IssuedToWarehouse = new Warehouse();
    switch (ProductCode.Substring(0,1))
    {
        case "A":
            IssuedToWarehouse.Code = "FM";
            IssuedToWarehouse.Name = "Fast movers";
            IssuedToWarehouse.Bin = "A";
            IssuedToWarehouse.BinReorderLevel = 10000;
            IssuedToWarehouse.LastStockTake = Convert.ToDateTime("2015-09-01");
            break;
        case "B":
            IssuedToWarehouse.Code = "FG";
            IssuedToWarehouse.Name = "Finished Goods";
            IssuedToWarehouse.Bin = "B";
            IssuedToWarehouse.BinReorderLevel = 500;
            IssuedToWarehouse.LastStockTake = Convert.ToDateTime("2015-09-04");
            break;
        case "C":
            IssuedToWarehouse.Code = "RM";
            IssuedToWarehouse.Name = "Raw Materials";
            IssuedToWarehouse.Bin = "AD";
            IssuedToWarehouse.BinReorderLevel = 7500;
            IssuedToWarehouse.LastStockTake = Convert.ToDateTime("2015-09-02");
            break;
        default:
            IssuedToWarehouse.Code = "GS";
            IssuedToWarehouse.Name = "General Stock";
            IssuedToWarehouse.Bin = "SS";
            IssuedToWarehouse.BinReorderLevel = 5000;
            IssuedToWarehouse.LastStockTake = Convert.ToDateTime("2015-09-09");
            break;
    }
    return IssuedToWarehouse;
}
```

*Code Listing 6: Warehouse Issue Logic*

You can see how postconditions can be used in Code Contracts to create highly robust code. Think of a developer working in a distributed team. Being able to work from anywhere in the world has many advantages and disadvantages (depending on your point of view). The absence of personal, one-to-one communication can be construed as a distinct disadvantage. Not being able to sit in a boardroom where developers can flesh out a problem together remains a challenge. Your brain can subconsciously infer feelings, meanings, and viewpoints based on the multitude of other signals (such as body language, eye movement, or breathing) that we tend to give out.

Communication is more than just the act of speaking. Therefore, as developers, we need to become sharper and heighten our effectiveness in other areas. A great place to start is at the code. With Code Contracts, we are able to defensively preempt certain conditions that may occur. Just because the specification doesn’t explicitly mention that a null condition would break the integration, that doesn’t mean we don’t need to defend against it.
