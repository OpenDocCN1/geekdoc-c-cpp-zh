# Software Engineering Observation 26.4

Any GUI components that will be manipulated by SwingWorker methods, such as components that will be updated from methods process or done, should be passed to the SwingWorker subclass’s constructor and stored in the subclass object. This gives these methods access to the GUI components they’ll manipulate.

When method execute is called on a BackgroundCalculator object, the object is scheduled for execution in a worker thread. Method doInBackground is called from the worker thread and invokes the fibonacci method (lines 46–52), passing instance variable n as an argument (line 23). Method fibonacci uses recursion to compute the Fibonacci of n. When fibonacci returns, method doInBackground returns the result.

After doInBackground returns, method done is called from the event dispatch thread. This method attempts to set the result JLabel to the return value of doInBackground by calling method get to retrieve this return value (line 32). Method get waits for the result to be ready if necessary, but since we call it from method done, the computation will be complete before get is called. Lines 34–37 catch InterruptedException if the current thread is interrupted while waiting for get to return. This exception will not occur in this example since the calculation will have already completed by the time get is called. Lines 38–42 catch ExecutionException, which is thrown if an exception occurs during the computation.

# Class FibonacciNumbers

Class FibonacciNumbers (Fig. 26.25) displays a window containing two sets of GUI components—one set to compute a Fibonacci number in a worker thread and another to get the next Fibonacci number in response to the user’s clicking a JButton. The constructor (lines 38–109) places these components in separate titled JPanels. Lines 46–47 and 78–79 add two JLabels, a JTextField and a JButton to the workerJPanel to allow the user to enter an integer whose Fibonacci number will be calculated by the BackgroundWorker. Lines 84–85 and 103 add two JLabels and a JButton to the event dispatch thread panel to allow the user to get the next Fibonacci number in the sequence. Instance variables n1 and n2 contain the previous two Fibonacci numbers in the sequence and are initialized to 0 and 1, respectively (lines 29–30). Instance variable count stores the most recently computed sequence number and is initialized to 1 (line 31). The two JLabels display count and n2 initially, so that the user will see the text Fibonacci of 1: 1 in the eventThreadJPanel when the GUI starts.

```
1  // Fig. 26.25: FibonacciNumbers.java
2  // Using SwingWorker to perform a long calculation with
3  // results displayed in a GUI.
4  import java.awt.GridLayout;
5  import java.awt.event.ActionEvent;
6  import java.awt.event.ActionListener;
7  import javax.swing.JButton;
8  import javax.swing.JFrame;
9  import javax.swing.JPanel;
```

Fig. 26.25 | Using SwingWorker to perform a long calculation with results displayed in a GUI. (Part 1 of 4.)