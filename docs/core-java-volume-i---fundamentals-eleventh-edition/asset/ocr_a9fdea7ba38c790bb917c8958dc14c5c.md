Install event handlers to be notified when the task is scheduled, starts running, and when it terminates with success, due to an exception, or due to cancellation. All handlers are executed on the UI thread.

```
task.scheduled(event -> cancel.setDisable(false));
task.setOnRunning(event -> status.setText("Running"));
task.setOnSucceeded(event -> status.setText("Read " + task.getValue() + " lines"));
task.setOnFailed(event -> status.setText("Failed due to " + task.getException()));
task.setOnCancelled(event -> status.setText("Canceled"));
```

The program in Listing 13.21 has commands for opening a text file and for canceling the file loading process. You should try the program with a long file, such as the full text of *The Count of Monte Cristo*, supplied in the gutenberg directory of the book’s companion code. The file is loaded in a separate thread. While the file is being read, the Open button is disabled and the Cancel button is enabled (see Figure 13.35). After each line is read, a line counter in the status bar is updated. After reading process is complete, the Open button is reenabled, the Cancel button is disabled, and the status line text is set to a “Done” message. We added a delay of 10 milliseconds between lines so that you can clearly observe the status updates. You would not do this in your own programs.

![](bbox=[0.246, 0.515, 0.841, 0.752])

**Figure 13.35** Reading lines from a web page in a worker thread

Pay close attention to what happens on the worker thread and the UI thread:

+   - The call method is executed on the worker thread.
+   - The lambda passed to `Platform.runLater` is executed on the UI thread.
+   - The handlers for the “on scheduled,” “on running,” “on failed,” “on cancelled,” and “on succeeded” events are executed on the UI thread.