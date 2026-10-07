# CHAPTER 14: Introducing the Xcode Debugg

It's important to note that not is only the debugger in the Bookstore object, but the debugger has also moved to the Bookstore.m file (it used to be in the MasterViewController.m file).

The control, Step Over, continues execution of the program, but doesn't go into a method. It simply executes the method and continues to the next line. Step Out, is a little like the opposite of Step Into. If the Step Out button is clicked, the current method continues execution until it finishes. The debugger then returns to the line before Step Into was clicked. For example, if the Step Into is clicked on the line shown in Figure 14–9 and then the Step Out button is clicked, the debugger will return to the ViewController.m file on the statement shown in Figure 14–9 (line 25 in the example), the line where the Step Into was made.

# Looking at the Thread Window and Call Stack

As mentioned, the thread window displays the current thread (there is only one in our program). However, it also displays the call stack. If we look at far as the difference between Figures 14–9 and 14–10 as the thread window goes, we can see that Figure 14–10 now has the [Bookstore init] method listed because [MasterViewController initWithNibName:bundle:] calls the [Bookstore init] method.

Now, the call stack is not simply a list of functions that have been called; rather, it's a list of functions that are currently being called. That's a very important distinction. Once the init method is finished and returns it no longer appear in the call stack. You can think of a call stack almost like a breadcrumb trail. The trail shows us how to get back to where we started.

# Debugging Variables

It is possible to view information about a variable (other than its memory address) by hovering over the variable. In our current example of the Bookstore, all the variables are synthesized properties. The problem is that they are not visible through the debugger. So, in order for the debugger to actually show these variables, we'll have to explicitly declare them. To do this, simply navigate to the Book.h header file and add an instance variable called titled, as shown in Figure 14–11.