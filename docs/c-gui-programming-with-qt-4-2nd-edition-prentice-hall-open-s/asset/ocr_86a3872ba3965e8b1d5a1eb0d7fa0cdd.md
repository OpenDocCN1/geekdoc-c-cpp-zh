# Communicating with the Main Thread

When a Qt application starts, only one thread is running—the main thread. This is the only thread that is allowed to create the QApplication or QCoreApplication object and call exec() on it. After the call to exec(), this thread is either waiting for an event or processing an event.

The main thread can start new threads by creating objects of a Thread subclass, as we did in the previous section. If these new threads need to communicate among themselves, they can use shared variables together with mutexes, read-write locks, semaphores, or wait conditions. But none of these techniques can be used to communicate with the main thread, since they would lock the event loop and freeze the user interface.

The solution for communicating from a secondary thread to the main thread is to use signal–slot connections across threads. Normally, the signals and slots mechanism operates synchronously, meaning that the slots connected to a signal are invoked immediately when the signal is emitted, with a direct function call.

However, when we connect objects "live" in different threads, the mechanism becomes asynchronous. (This Behavior can be changed through an optional fifth parameter to QObject::connect()) Behind the scenes, these connections are implemented by posting an event. The slot is then called by the event loop of the thread in which the receiver object exists. By default, a QObject exists in the thread in which it was created; this can be changed at any time by calling QObject::moveToThread().

To illustrate how signal–slot connections across threads work, we will review the code of the Image Pro application, a basic image processing application that allows the user to rotate, resize, and change the color depth of an image. The application (shown in Figure 14.3), uses one secondary thread to perform operations on images without locking the event loop. This makes a significant difference when processing very large images. The secondary thread has a list of tasks, or "transactions", to accomplish and sends events to the main window to report progress.

```
ImageWindow::ImageWindow()
{
    imageLabel = new QLabel;
    imageLabel->setBackgroundRole(QPalette::Dark);
    imageLabel->setAutoFillBackground(true);
    imageLabel->setAlignment(Qt::AlignLeft | Qt::AlignTop);
    setCentralWidget(imageLabel);

    createActions();
    createMenus();
```