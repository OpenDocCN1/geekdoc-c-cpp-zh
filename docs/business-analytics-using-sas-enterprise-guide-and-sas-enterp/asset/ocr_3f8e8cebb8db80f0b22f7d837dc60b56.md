# ## Model

Now the fun really begins. The first model is a decision tree. Because the decision tree process finds discrete groupings to build the model, this modeling process will not use the transformed variables.

# ### Decision Tree

In Chapter 8, you built a decision tree to describe the data. In this chapter, you are building a decision tree to predict the likelihood of an event occurring. This method is versatile and can be used in multiple ways.

> > **NOTE:** Recall that you replaced the missing values in your data using the Impute function. If you had not replaced these values, the Decision Tree process would treat them as a separate category. See Enterprise Guide Help Contents for more information.

Under the **Model** tab, drag the **Decision Tree** icon onto the diagram and connect it to the **Filter** node as shown in Figure 9.13. Two changes are recommended in the **Property** window. Under **Splitting Rule**, change the **Maximum Branch** to 4. This option is something you can explore, going higher and lower. Under **Subtree**, change the **Method** to **Assessment** and the **Assessment Measure** to **Lift**. Right-click the **Decision Tree** icon and click **Run** ➤ **Yes**.

**Figure 9.13: Decision Tree Property Window**

![](bbox=[0.118, 0.452, 0.947, 0.796])

Once the run completes, click **Results**. The graph in the upper left corner of the output window shows the cumulative lift graph as seen in Output 9.9. The graph shows that the lift in the train data is much better than the lift in the validation data.