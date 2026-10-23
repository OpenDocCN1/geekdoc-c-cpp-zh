When the report appears, you are presented with a control panel, used to specify how effects should enter or exit the model. In this example, we to add any effects that are significant at the 0.25 level or better.

Leave 0.25 as the Prob to Enter.

We now have a choice of three stepwise methods: Forward (where effects are added as they become significant), Backward (where effects are removed as they become noon-significant) or Mixed, a combination of the two detailed below. This example uses forward selection, so

Leave the default Forward selection method.

We now want to add significant effects. To add the first detected effect,

Click the Step button.

After one step, the most significant term Runtime is entered into the model (top Current Estimates table in Figure 6.3).

To automatically add all the detected effects automatically (rather than manually with the Step button)

Click Go to see the stepwise process run to completion.

The bottom table in Figure 6.3 shows that all the terms have been added except RstPulse and Weight which are not significant at the Prob to Enter value of 0.25 specified in the Stepwise Regression Control Panel.

# Figure 6.3 Current Estimates Table

![](bbox=[0.24, 0.52, 0.8, 0.75])

Now that we have selected the effects that contribute to explaining Oxy, we can make a model and examine its analysis.

Click Make Model.

A Fit Model dialog appears.

Click Run Model.

This produces a report identical to those seen in “The Fit Model Platform” chapter.