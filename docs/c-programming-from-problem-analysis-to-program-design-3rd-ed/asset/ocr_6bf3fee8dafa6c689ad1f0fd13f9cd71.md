The problem specification indicates that only valid states along the Atlantic ICW should be entered into the application. An object of the `TestOfStateException` `class` is thrown if the `ShoalArea` objects' state data member is assigned an invalid value for the state. The message property of the `Exception` `class` is displayed in a label named `lblError` on the form object. These points are shown in Figure 12-29.

![](bbox=[0.189, 0.215, 0.502, 0.478])

# Figure 12-29 State exception thrown inWaterDept application

As you review the program statements, notice that several `catch` clauses were included. Figure 12-30 shows the message displayed in the `lblError` when the user attempts to enter a nonnumeric value for the mile marker.

![](bbox=[0.189, 0.626, 0.503, 0.884])

# Figure 12-30 Invalid input exception thrown in WaterDept application