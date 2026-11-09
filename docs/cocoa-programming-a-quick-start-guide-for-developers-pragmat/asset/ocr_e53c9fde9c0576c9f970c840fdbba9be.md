# The family of NSControllers

NSObjectController extends from the abstract class NSController. Here is a family portrait of the NSObjectController and its siblings:

![](bbox=[0.237, 0.176, 0.679, 0.499])

Start with a little cleanup. Remove the two sliders from the interface, and add another stepper and text field. I removed the number formatter, but you don’t need to do so. You can speed this step by selecting the existing stepper and text field, duplicating them using ⌘ D, and placing the new items where you want them.

Use the Identity inspector to change the names of the Counter and NSObjectController to Counter1 and CounterController1, respectively.

Drag a Counter object from the Library to the Document window, and change its and its name to Counter2. Drag a new object controller in from the Library, and change its name to CounterController2.

Now just follow the steps you did before. Select the CounterController2, and use the Connections inspector to connect the content outlet to Counter2. Switch to the Attributes inspector, set the class to Counter, and add the count key.