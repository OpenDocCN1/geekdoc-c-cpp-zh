To make the worker do some useful job, events have to be implemented. There are three such events in total, as shown in Figure 29.27. We implement all three of them, serving the following roles:

+   - DoWork is triggered when someone calls RunWorkerAsync. The DoWork event handler will be run on a thread different from the one that called the RunWorkerAsync method, resulting in asynchrony.
+   - ProgressChanged is called every time the worker updates its progress from code running under the DoWork handler. This event handler is invoked on the synchronization context of the requester, in this case the UI thread. In other words, one can safely update the user interface from this handler.
+   - RunWorkerCompleted is similar to the ProgressChanged event with regard to where it gets run. It's triggered by the worker thread signaling completion.

![](bbox=[0.06, 0.5, 0.44, 0.67])

FIGURE 29.27 Events on a BackgroundWorker component.

Using the BackgroundWorker component, we now create an asynchronous block-based file copy tool. It simply uses two FileStream objects to read from and write to the source and destination files, respectively. All the copying logic is done from the DoWork event handler, which takes place in the background, relative to the UI thread where the user triggers the copy command. We omit a discussion of UI design and refer to Figure 29.28 for a possible interface including a few labels, text boxes, buttons, a numeric up/down control, and a progress bar.

![](bbox=[0.06, 0.8, 0.44, 0.95])

FIGURE 29.28 Our asynchronous file copy tool in action.