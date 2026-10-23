# Figure 5.12 Expanded Estimates Table

![](bbox=[0.262, 0.115, 0.744, 0.255])

Compare the expanded estimates with the prediction formula for this model, shown here.

```
16.9641526057058
+Match(Method) {"Alpha Amalyze" => -6.1326090308367, "Caustic Soda" => 4.55240663376582, "Pumice Stone" => 1.58020239707087, else => .}
+0.0465825281069*Size of Load (lbs)
+Match(Sand blasted?) {"no" => -1.8002952999013, "yes" => 1.80029529990132, else => .}
```

# Custom Test

In introductory statistics courses, null hypotheses are often about one variable at a time, frequently hypothesizing that a parameter is zero. However, it is possible to test far more complicated null hypotheses than this. For example, it is reasonable to test that several parameters are zero, one, or another value, or that some parameters are equal to others. These tests are known in statistics as a general linear hypotheses, and are tested using JMP's Custom Test command.

To test a custom hypothesis, select Custom Test from the Estimates popup menu, which displays the dialog shown in Figure 5.13.

# Figure 5.13 Custom Test Launch

You can enter a descriptive label for this test—useful if you are doing several tests

![](bbox=[0.468, 0.668, 0.754, 0.855])

The space beneath the Custom Test title bar is an editable area for entering a test name.