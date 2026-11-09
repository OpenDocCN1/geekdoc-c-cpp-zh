2. Open the Code Editor window, then locate the code template for the btnDisplay control's Click event procedure. First, declare the two-dimensional array. Click the **blank line** below the ' declare the two-dimensional array comment. Enter the array declaration statement shown in Figure 21-11, then position the insertion point as shown in the figure.

![](bbox=[0.1, 0.24, 0.92, 0.42])

**Figure 21-11:** Array declaration entered in the procedure

3. The procedure will need an accumulator variable to total the orders. Type **dim intTotal as integer**, press **Tab**, then type **' accumulator** and press **Enter**.

4. To accumulate the values stored in the array, you will need to access each array element. As mentioned earlier, you do this using both an outer loop and a nested loop. You can access the elements either row by row or column by column; in this case, you will access them column by column. Click the **blank line** below the ' accumulate the calendars ordered comment. Enter the two repetition structures shown in Figure 21-12.

![](bbox=[0.12, 0.625, 0.92, 0.735])

**Figure 21-12:** Repetition structures entered in the procedure

5. Finally, display the total number of calendars ordered. Click the **blank line** below the 'display the number of calendars ordered comment. Type **lblTotal.text = intTotal.tostring** and press **Enter**.

6. Save the solution, then start the application. Click the **Display Total** button. The total number of calendars ordered appears in the Total ordered box, as shown in Figure 21-13.