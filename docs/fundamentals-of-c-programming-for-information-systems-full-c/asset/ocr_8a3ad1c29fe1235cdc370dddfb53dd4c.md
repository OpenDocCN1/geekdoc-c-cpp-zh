# Review Questions

+   5.1 What is a method?
+   5.2 What is an event handler?
+   5.3 True or false: A method typically performs a subtask that is a part of a larger or more complex task.
+   5.4 True or false: A method can be called from multiple methods.
+   5.5 Write the statement to call a method named, ComputeCost.

# 5.2 Passing Values to Methods

The previous method, DisplayInfo, did not need any input data to be provided by the calling program to display its output. However, it often is necessary to pass input data to a method from the calling program. To help understand passing data to methods, you will develop a method, ComputeTrainingRate(), to compute your training heart rate using your age and resting rate, and display the rate in a MessageBox, as shown in Figure 5-5.

Figure 5-5: The HeartRate form with Training Rate MessageBox

![](bbox=[0.175, 0.445, 0.875, 0.67])

The age and resting rate are passed by the calling program to ComputeTrainingRate(). Figure 5-6 depicts the structure chart that shows the calling and called programs and the data transferred between them.

Figure 5-6: Structure chart of program to compute training rate

![](bbox=[0.135, 0.76, 0.405, 0.9])