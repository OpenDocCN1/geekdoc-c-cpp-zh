![](bbox=[0.28, 0.15, 0.94, 0.48])

FIGURE 8.3 Creating a nib-based view controller

To create a pop-up view, add a new UIViewController subclass to the project. In the options panel, make sure the "With XIB for user interface" check box is selected (Figure 8.3). This will create our class header, an implementation file, and an initial nib file.

Then open PauseViewController.xib. Working with a nib is almost the same as working with a storyboard. However, we will find a few differences. The scene list is gone, as is the scene dock. Instead, we have a single dock that holds the top-level objects for the entire nib. Meanwhile, the Interface Builder area simply displays our top-level views.

Our nib starts with three top-level objects: the File's Owner, the first responder, and our view (Figure 8.4). Of the three, only the File's Owner is new. Like the first responder, it is a placeholder (also sometimes called a proxy object). The system does not instantiate the placeholders when we load the nib. Instead, we instantiate an instance of the File's Owner in our code and then pass it to the nib-loading method. This is implicitly handled for us when we call UIViewController's initWithNibName:bundle: method. Our newly instantiated controller will be passed to the nib-loading code, which will in turn set up and configure our controller. The File's Owner represents the main link between the nib and the rest of your application. In our case, the File's Owner is our PauseViewController instance.