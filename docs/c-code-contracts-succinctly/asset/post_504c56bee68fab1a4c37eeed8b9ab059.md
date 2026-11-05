
~~~csharp
Assert.AreEqual<int>(0, i);
Assert.IsNotNull((object)eRPWarehouseIntegration);
Assert.AreEqual<int>(0, eRPWarehouseIntegration.MaxBinQuantity);
Assert.AreEqual<int>(0, eRPWarehouseIntegration.CurrentBinQuantity);
}
~~~

*Code Listing 63: Generated Code in Details*

Looking at the **Details** node, we can see the generated code for the unit test.

## Test 1: Failed, DivideByZeroException

Looking at Test 1, we can see that it failed because it tried to divide by zero.

IntelliTest Exploration Results - stopped

ERPWarehouseIntegrationTest.Pro — 1 Warnings — 10/15 blocks, 1/1 asserts, 4 runs

| # | target | binVolume | factor | result(target) | result | Summary / Exception | Error Message |
|---|---|---|---|---|---|---|---|
| 1 | new ERPWa... | 0 | 0 |  |  | DivideByZeroException | Attempted to divide by zero. |
| 2 | new ERPWa... | 0 | 1 | new ERPWar... | 0 | ContractException | Postcondition failed: Contract.Result<int>() ... |
| 3 | new ERPWa... | 1 | 386 |  |  | ContractException | Arithmetic operation resulted in an overflow. |
| 4 | new ERPWa... | int.MinValue | -1 |  |  | OverflowException | Arithmetic operation resulted in an overflow. |

*Figure 51: Divide by Zero Exception*

This means that we forgot to take care of a factor value of zero. If you look at the **CutSteel()** method you will see that we are dealing with a modulus and not a divisor. So how can we have a divide by zero exception? Well the rule of thumb is that if the second operand of a / or a % is zero, we will have a divide by zero exception.

## Test 3: Failed, ContractException

Test 3 failed because the Code Contract ensures a result that the method isn't adhering to. Remember, the **ProductionVolumePerBin()** method ensures that the bin volume is returned to the calling code, which signifies that we have produced a perfect cut with zero scrap. The test failed, and in a production environment this situation will happen. Our Code Contract ensures that the result returned by the method will always equal the bin volume. This means that we need to deal with the eventuality of an imperfect cut.

## Test 4: Failed, OverflowException

The last failed test is rather interesting. We can see that the test was passed **int.MinValue** for **binVolume**. According to the MSDN documentation, **int.MinValue** represents the smallest possible value for **Int32**. It is also a constant with a value of **-2,147,483,648**. The factor has a value of **-1** and the modulus results in an **OverflowException**. This means that our code in the **CutSteel()** method will effectively be **int.MinValue % -1**; and this fails our test.

The reason that this happens is because the C# language specification implements it as such. In **7.8.3 Remainder operator** of the **C# Language Specification** it states: "If the left operand is the smallest int or long value and the right operand is -1, a System.OverflowException is thrown."

> **Note:** If you would like to dig a little deeper, you can view this thread on StackOverflow for a very good explanation on why this is implemented this way in C#.

## Fixing test failures

We can see from the previous IntelliTests that there are some loopholes in our **ProductionVolumePerBin()** method. These need fixing, and the most obvious one to fix is the divide by zero exception. Let's add a **Contract.Requires()** to our method to only allow factor values greater than 1.

```csharp
/// <summary>
/// Calculate the production volume of steel per bin
/// </summary>
/// <param name="binVolume"></param>
/// <param name="factor"></param>
/// <returns>Bin Volume less Remainder</returns>
public int ProductionVolumePerBin(int binVolume, int factor)
{
    Contract.Requires(factor > 1,
        "The supplied cutting factor must be more than the value 1.");
    Contract.Ensures(Contract.Result<int>() == binVolume,
        "The factor used will result in scrap. Please modify the cutting factor.");

    int remainder = CutSteel(binVolume, factor);
    return binVolume - remainder;
}
```

*Code Listing 64: Modified Code to Ensure Valid Integers*

After adding the **Contract.Requires()** precondition, the method will only allow valid cutting factor values. Run the IntelliTest again by right-clicking on the **ProductionVolumePerBin()** method and selecting **Run IntelliTest** from the context menu.

![](img/0a07386735fd4e6427d20aa9bc165f5d_75_0.png)

*Figure 52: IntelliTest Results after Valid Integer Change*

The results of the test are quite different. Our contract preconditions are working correctly and limiting the erroneous values from being passed to our method. However, we can see that the IntelliTest passed a **binVolume** value significantly smaller than the **factor** value. Let us work on this issue first by requiring the **binVolume** value to never be smaller than the **factor** value.

```csharp
/// <summary>
/// Calculate the production volume of steel per bin
/// </summary>
/// <param name="binVolume"></param>
/// <param name="factor"></param>
/// <returns>Bin Volume less Remainder</returns>
public int ProductionVolumePerBin(int binVolume, int factor)
{
    Contract.Requires(factor > 1,
        "The supplied cutting factor must be more than the value 1.");
    Contract.Requires(binVolume > factor,
        "The cutting factor cannot be greater than the bin volume");
    Contract.Ensures(Contract.Result<int>() == binVolume,
        "The factor used will result in scrap. Please modify the cutting factor.");

    int remainder = CutSteel(binVolume, factor);
    return binVolume - remainder;
}
```

*Code Listing 65: Modified Code to Ensure Valid Cutting Factor*

To achieve this, we need to add another **Contract.Requires()** pre-condition that will require that the **binVolume** value is always greater than the **factor** value. Run the IntelliTest again from the context menu.

![](img/0a07386735fd4e6427d20aa9bc165f5d_76_0.png)

*Figure 53: IntelliTest Results after Valid Cutting Factor Change*

The results returned from this test tell us that the only issue we are experiencing with the **ProductionVolumePerBin()** method is that it still fails on the value being returned. Our method guarantees the calling code that it will return a perfect cut every time, and it is failing this contract. We might want to consider adding a bit more intelligence to this method by letting our code suggest a valid cutting factor to the user if the supplied one is not valid.

/// <summary>
/// The new valid cutting factor calculated by ProductionVolumePerBin
/// </summary>
public int CalculatedCuttingFactor { get; private set; } = 0;

/// <summary>
/// Calculate the production volume of steel per bin
/// </summary>
/// <param name="binVolume"></param>
/// <param name="factor"></param>
/// <returns>Bin Volume less Remainder</returns>
public int ProductionVolumePerBin(int binVolume, int factor)
{
    Contract.Requires(IsEven(binVolume),
        "Invalid bin volume entered");
    Contract.Requires(factor > 1,
        "The supplied cutting factor must be more than the value 1.");
    Contract.Requires(binVolume > factor,
        "The cutting factor cannot be greater than the bin volume");
    Contract.Ensures(Contract.Result<int>() == binVolume,
        "The factor used will result in scrap. Please modify the cutting factor.");

    int remainder = CutSteel(binVolume, factor);
    while ((binVolume - remainder) != binVolume)
    {
        CalculatedCuttingFactor = CalculateNewCutFactor(binVolume);
        remainder = CutSteel(binVolume, CalculatedCuttingFactor);
    }

    return binVolume - remainder;
}

/// <summary>
/// Calculate any remainder after the modulus operation between volume and factor
/// </summary>
/// <param name="volumeToCut"></param>
/// <param name="factor"></param>
/// <returns>Remainder after cutting</returns>
private int CutSteel(int volumeToCut, int factor)
{
    // Use modulus to determine if the factor produces any scrap
    return volumeToCut % factor;
}

/// <summary>
