When the user clicks the button for thread A, startOrStopThreadA() stops the thread if it was running and starts it otherwise. It also updates the button's text.

```
void ThreadDialog::startOrStopThreadB()\{
  if (threadB.isRunning()) {
    threadB.stop();
    threadBButton->setText(tr("Start B"));
  } else {
    threadB.start();
    threadBButton->setText(tr("Stop B"));
  }
}
```

The code for startOrStopThreadB() is structurally identical.

```
void ThreadDialog::closeEvent(QCloseEvent *event)
{
  threadA.stop();
  threadB.stop();
  threadA.wait();
  threadB.wait();
  event->accept();
}
```

If the user clicks Quit or closes the window, we stop any running threads and wait for them to finish (using QThread::wait()) before we call QCloseEvent::accept(). This ensures that the application exits in a clean state, although it doesn't really matter in this example.

If you run the application and click Start A, the console will be filled with 'A's. If you click Start B, it will now fill with alternating sequences of 'A's and 'B's. Click Stop A, and now it will print only 'B's.