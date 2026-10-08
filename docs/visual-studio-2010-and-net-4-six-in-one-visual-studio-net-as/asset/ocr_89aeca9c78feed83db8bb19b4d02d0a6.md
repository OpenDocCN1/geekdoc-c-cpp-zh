> Statistical operations generally result in scalar values, or very simple structures. Check out the MSDN documentation of the StatisticalFormula class (this is the type behind the Statistics property) for operations you can use with chart data at http://msdn.microsoft.com/en-us/library/system.windows.forms.datavisualization.charting.statisticalformula_members(US.100).aspx.

# Apply Financial Formula to Data

To perform financial analysis on one or more Series objects, use the FinancialFormula method of the DataManipulator class. FinancialFormula has many overloads, as well as each of them having the same structure:

+   **Formula name** — Specify the type of formula here with a FinancialFormula enumeration value. Number of parameters, input, and output, as well as the requirements for each parameter, based on the formula you choose
- **Parameters** — Some formulas require parameters, and enable you to optionally supply them. A few do not use parameters. If a formula takes multiple parameters, specify them as a comma-separated string (for example, "3,5").
- **Input values** — Specify in a comma-separated string the names of instantiated Series objects to which you want to save the output. If you do not specify output values, the formula stores the first output value in the first listed input, and so on. In this case, the method throws an exception if the number of input values is less than the number of output values.
- **Optional output values** — Specify in a comma-separated string the name of instantiated Series objects to which you want to save.

The following code snippet calculates a moving average from Series1, and puts the results in Series2:

```
private void ApplyButtonItemClick(object sender, EventArgs e)
chart1.DataManipulator.FinancialFormula(
    "5",
    FinancialFormula.MovingAverage,
    "Series1",
    "Series2";
)
```

The second argument, 5, defines the number of samples to use to calculate the moving average. Figure 14-52 shows the result of the operation.