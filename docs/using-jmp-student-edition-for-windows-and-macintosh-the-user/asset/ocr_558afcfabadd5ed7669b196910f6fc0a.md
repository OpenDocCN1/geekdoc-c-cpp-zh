# Mask Color

displays the JMP color palette for you to select a line color for the V-mask.

# Connect Color

displays the JMP color palette for you to select a color for the connect line when the **Connect Points** option is in effect.

# Center Line Color

displays the JMP color palette for you to select a color for the center line.

# Show Shift

shows or hides the shift you entered, or center line.

# Show V Mask

shows or hides the V-mask based on the parameters (statistics) specified on the Control Charts Launch dialog when Cusum is selected as the Chart Type.

# Show Parameters

displays a Parameters table (see Figure 7.26) that summarizes the Cusum charting parameters.

# Show ARL

displays the average run length (ARL) information.

# Example 1. Two-Sided Cusum Chart with V-mask

To see an example of a two-sided cusum chart, open the Oil1 Cusum.jmp file from the Quality Control sample data folder. A machine fills 8-ounce cans of two-cycle engine oil additive. The filling process is believed to be in statistical control. The process is set so that the average weight of a filled can, μ₀, is 8.10 ounces. Previous analysis shows that the standard deviation of fill weights, σ₀, is 0.05 ounces.

Subgroup samples of four cans are selected and weighed every hour for twelve hours. Each observation in the Oil1 Cusum.jmp data table contains one value of weight along with its associated value of hour. The observations are sorted so that the values of hour are in increasing order. The Control Chart platform assumes that the data are sorted in increasing order.

A two-sided cusum chart is used to detect shifts of at least one standard deviation in either direction from the target mean of 8.10 ounces.

To create a Cusum chart for this example,

+   - Choose the **Graph > Control Chart > CUSUM** command.
+   - Click the **Two Sided** check box if it is not already checked.
+   - Specify weight as the Process variable.
+   - Specify hour as the Sample Label.
+   - Click the **H** radio button and enter 2 into the text box.