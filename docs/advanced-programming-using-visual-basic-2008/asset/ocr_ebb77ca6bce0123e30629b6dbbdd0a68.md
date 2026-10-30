# Feedback 13.4

+   1. My.Application.ChangeUICulture("fr-FR")
+   2. The statement should be placed in the Sub New() procedure.

# Feedback 13.5

+   1. The code for background processing may be placed in any procedure.
+   2. BackgroundWorker1.RunWorkerAsync()
+   3. Use the BackgroundWorker.CancellationPending method in the DoWork event handler. Call the CancelAsync method to cancel the operation in the event handler for the Cancel button. In the RunWorkerCompleted event handler, check for e.Cancelled.