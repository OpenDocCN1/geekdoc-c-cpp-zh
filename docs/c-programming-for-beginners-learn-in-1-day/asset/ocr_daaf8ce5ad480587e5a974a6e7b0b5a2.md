The code will be written to our Program.cs file. In the below program, we will write the code to see how we can use the above-mentioned methods.

In this example, we will see how a queue gets created. Next, we will see how to display the elements of the queue, and use the Count and Contain methods.

![](bbox=[0.05, 0.23, 0.95, 0.65])

# Code Explanation:-

+   1. The first step is used to declare the Queue. Here we are declaring qt as a variable to hold the elements of our Queue.
+   2. Next, we add 3 elements to our Queue. Each element is added via the “enqueue” method.
+   3. Now one thing that needs to be noted about Queues is that the elements cannot be accessed via the index position like the array list. We need to use a different approach to display the elements of the Queue. So here’s how we go about displaying the elements of a queue.
+      - We first declare a temporary variable called obj. This will be used to hold each element of the Queue.
+      - We then use the foreach statement to go through each element of the Queue.
+      - For each Queue element, the value is assigned to the obj variable.
+      - We then use the Console.Writeline command to display the value to the console.
+   4. We are using the “Count” property to get the number of items in the Queue. This property will return a number. We then display this value to the console.