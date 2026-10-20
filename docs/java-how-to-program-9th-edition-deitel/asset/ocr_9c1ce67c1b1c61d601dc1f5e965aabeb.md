doInBackground and done methods. Method doInBackground performs the computation and returns the result. Method done displays the results in the GUI.

+   - Class SwingWorker’s first type parameter indicates the type returned by the doInBackground method; the second indicates the type that’s passed between the publish and process methods to handle intermediate results.
+   - Method doInBackground is called from a worker thread. After doInBackground returns, method done is called from the event dispatch thread to display the results.
+   - An ExecutionException is thrown if an exception occurs during the computation.
+   - SwingWorker method publish repeatedly sends intermediate results to method process, which displays the results in a GUI component. Method setProgress updates the progress property.
+   - Method process executes in the event dispatch thread and receives data from method publish. The passing of values between publish in the worker thread and process in the event dispatch thread is asynchronous; process is not necessarily invoked for every call to publish.
+   - PropertyChangeListener (p. 1108) is an interface from package java.beans that defines a single method, propertyChange. Every time method setProgress is invoked, a PropertyChangeEvent is generated to indicate that the progress property has changed.



+   - The Callable (p. 1109) interface (of package java.util.concurrent) declares a single method named call that allows the thread to return a value or to throw a checked exception.
+   - ExecutorService method submit (p. 1109) executes a Callable passed in as its argument.
+   - Method submit returns an object of type Future (of package java.util.concurrent) that represents the executing Callable. Interface Future (p. 1109) declares method get to return the result of the Callable and provides other methods to manage a Callable’s execution.



Java SE 7’s concurrency APIs include the new fork/join framework, which helps programmers parallelize algorithms. The fork/join framework is particularly well suited to divide-and-conquer-style algorithms, like the merge sort.



26.1 Fill in the blanks in each of the following statements:

+   a) A thread enters the terminated state when ________.
+   b) To pause for a designated number of milliseconds and resume execution, a thread should call method ________ of class ________.
+   c) Method ________ of class Condition moves a single thread in an object’s waiting state to the runnable state.
+   d) Method ________ of class Condition moves every thread in an object’s waiting state to the runnable state.
+   e) A(n) ________ thread enters the ________ state when it completes its task or otherwise terminates.
+   f) A runnable thread can enter the ________ state for a specified interval of time.
+   g) At the operating-system level, the runnable state actually encompasses two separate states, ________ and ________.
+   h) Runnables are executed using a class that implements the ________ interface.
+   i) ExecutorService method ________ ends each thread in an ExecutorService as soon as it finishes executing its current Runnable, if any.