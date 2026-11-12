+   3. Show that GT = TP+TN and that TAP = GT - TAN.
+   4. Show that Error Rate = 1 - Accuracy.
+   5. What do sensitivity and specificity measure?
+   6. Explain the Method for Model Evaluation.
+   7. Why did we choose the All Negative model as a baseline to calibrate the accuracy of Model 1, rather than the All Positive model?
+   8. When error costs are unequal, what is the most important evaluation measure for the purpose of model selection?
+   9. Explain how a naïve analyst would erroneously prefer Model 1 to Model 2.
+   10. For the All Positive and All Negative models, calculate the evaluation metrics from Table 7.11.

# WORKING WITH THE DATA

For Exercises 11–22, work with the clothing_data_driven_training and clothing_data_driven_test data sets. Use R to solve each problem.

+   11. Using the training data set, create a C5.0 model (Model 1) to predict a customer’s Response using Days since Purchase, # of Purchase Visits, and Sales per Visit. Obtain the predicted responses.
+   12. Evaluate Model 1 using the test data set. Construct a contingency table to compare the actual and predicted values of Response.
+   13. For Model 1, recapitulate Table 7.4 from the text, calculating all of the model evaluation measures shown in the table. Call this table the Model Evaluation Table. Leave space for Models 2 and 3.
+   14. Clearly and completely interpret each of the Model 1 evaluation measures from the Model Evaluation Table.
+   15. Create a cost matrix, called the 4x cost matrix, that specifies a false positive is four times as bad as a false negative.
+   16. Using the training data set, build a C5.0 model (Model 2) to predict a customer’s Response using Days since Purchase, # of Purchase Visits, and Sales per Visit, using the 4x cost matrix.
+   17. Evaluate your predictions from Model 2 using the actual response values from the test data set. Add Overall Model Cost and Profit per Customer to the Model Evaluation Table. Calculate all the measures from the Model Evaluation Table.
+   18. Compare the evaluation measures from Model 1 and Model 2 using the 4x cost matrix. Discuss the strengths and weaknesses of each model.
+   19. Construct the simplified data-driven cost matrix as follows:
+   a. Obtain the mean of the Sales per Visit variable from the training data set and set the negative of that value to be the “cost” of a true positive. Let the false positive cost equal $10.