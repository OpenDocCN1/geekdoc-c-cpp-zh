the residuals versus the cell means, this departure can be detected if the vertical scatter in the residuals increases from left to right on the plot.

# Figure 2.3 Plot of Response versus Factor Level for Bread Rise Experiment

![](bbox=[0.2, 0.17, 0.8, 0.45])

For the bread rise experiment, the SAS commands:

```
/* Fit model and Examine Residual Plots */
ods graphics on;
proc glm data=bread plots=diagnostics(unpack);
   class time;
   model height=time/solution;
   run;
ods graphics off;
```

will fit the model for the CRD design, and when the ods graphics are turned on as shown in this example, the option plots=diagnostics(unpack) creates a panel of diagnostic plots to determine whether the assumptions of the model are satisfied. The (unpack) feature separates the plots so that they can be individually displayed. One of the plots created in this panel is labeled Residuals by Predicted and is shown in Figure 2.4. For the CRD design with one factor, the predicted values from the model, y_ij_hat = mu_i_hat, are the cell means. As can be seen in Figure 2.4, there is a wider spread in the residuals for larger cell means or predicted values. This indicates that the equality of variance assumption may be violated. This fact is easier to see in Figure 2.4 than it was in Figure 2.3.

To verify the assumption of normality of the experimental error, a normal probability plot of the residuals can be examined. In the panel of diagnostic plots created by proc glm the normal probability plot is labeled Q-Q Plot of Residuals, and it is shown in Figure 2.5.