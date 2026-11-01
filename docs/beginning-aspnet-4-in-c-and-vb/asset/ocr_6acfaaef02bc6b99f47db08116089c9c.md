```
message.Recoverable = true;
queue.Send(message, String.Format("Course Order ({0})",
order.Customer.Company));
}
MessageBox.Show("Course Order submitted");
catch (MessageQueueException ex)
{
MessageBox.Show(ex.Message, "Course Order Error",
MessageBoxButton.OK, MessageBoxImage.Error);
}
```

code snippet CourseOrderSender/CourseOrderWindow.xaml.cs

By running the application, you can add course orders to the message queue (see Figure 46-11).

![](bbox=[0.12, 0.38, 0.55, 0.68])

FIGURE 46-11

![](bbox=[0.6, 0.42, 0.88, 0.65])

FIGURE 46-12

# Course Order Message Receiver

The design view of the Course Order receiving application that reads messages from the queue is shown in Figure 46-12. This application displays labels of every order in the listOrders list box. When an order is selected, the content of the order is displayed with the controls on the right side of the application.

In the constructor of the Window class CourseOrderReceiverWindow, the MessageQueue object is created that references the same queue that was used with the sending application. For reading messages, the XmlMessageFormatter with the types that are read is associated with the queue using the Formatter property.

To display the available messages in the list, a new task is created that peeks at messages in the background. The task's main method is PeekMessages.

```
using System;
using System.Messaging;
using System.Threading;
using System.Windows;
using System.Windows.Controls;
```