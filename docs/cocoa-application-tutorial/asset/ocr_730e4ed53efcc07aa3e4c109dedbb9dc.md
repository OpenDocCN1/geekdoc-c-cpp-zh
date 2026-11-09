+   2. Select the outlet that corresponds to the first field, `rateField` as shown in Figure 5-5.

**Figure 5-5**  Connecting `ConverterController` to the `rateField` outlet

![](bbox=[0.218, 0.172, 0.548, 0.504])

+   3. Following the same steps, connect the `ConverterController` class’s `dollarField` and `amountField` outlets to the appropriate text fields.

# Connect the Convert Button to the Appropriate Methods

To connect the user interface elements in the Currency Converter window to the methods of the `ConverterController` class:

+   1. Control-drag a connection from the Convert button to the `ConverterController` instance in the nib file window.
+   2. A black box will pop up similar to the one we used to connect outlets. Choose `convert:`.
+   3. Save the nib file.

# Check Your Work

To make sure everything is done correctly:

+   1. Select the Converter Controller instance in the MainMenu.nib window.