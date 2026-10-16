Windows Forms is a rich framework that helps build client applications that are easier to use, offer supportive tools, and lower costs of deployment. You will often see desktop apps in Windows termed as rich-client apps as a way of differentiating them from the web apps that are browser-based and downloaded from one central place. We find the classes for creating these rich-client apps in the System.Windows.Forms namespace and, collectively these are called the Windows Form Classes. Here, you will find the Form class, control classes, clipboard interaction classes, menu classes, printing classes, and many more.

# Using Forms as Dialog Boxes

One of the most common uses of forms is interactive dialog boxes. These can be very basic forms with nothing more than a text box control or the most elaborate of forms that contain multiple controls. Most of what we will be discussing here are those controls.

Some dialog box types are used so much that they now tend to be integrated into the operating system. Collectively known as common dialog boxes, these include the dialog boxes that are prebuilt to handle tasks like file selection, color specification, choosing fonts, printer settings configuration, and more. In the .NET framework, you will find several classes that give you access to those common boxes, and in the next few sections, we’ll cover those classes.

More often than not, we use dialog boxes to show users a notification message. Rather than every programmer having to develop their own dialog boxes for generic messages, Microsoft built message box control into the Windows operating system. This is a special dialog box that makes it much easier to show a user a simple text message and it includes several button layouts and icons that have been predefined for you. The .Net framework wraps this message box in a class called MessageBox, which we will cover later.

# Using Forms as Views