Now that the functions are written, we can write a test procedure to see if it works as expected. We know the three conditions that should result in a discount, and we’ll test the combinations of those. The Debug.Assert method will halt the code if a test doesn’t pass. For illustration purposes, there is an error in the IsLastDayOfMonth function. We’ll fix that error shortly. Figure 27.1 shows the test procedure after it has been run.

# FIGURE 27.1

Debug.Assert halts code when a test fails.

![](bbox=[0.17, 0.36, 0.83, 0.85])

To test the function, three arrays were created containing information to pass to the function. The vaCustomer array contains one customer that gets a discount and one customer that doesn’t. These customers were selected by inspecting the Customers table. The vaTotal