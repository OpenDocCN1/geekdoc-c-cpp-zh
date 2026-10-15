# Figure 32.30: Adding 10 Elements to the List<T> Object

You can click the Insert and Remove buttons to insert a new item or remove the item from the list, respectively. For instance, the item name, Purple is removed from the list, as shown in Figure 32.31:

# Figure 32.31: Removing an Element from the List<T> Object

You can click the Reverse button to reverse the order of the color names displayed in the ListBox control.

# Using the LinkedList<T> Class

In this section, you learn how to use the LinkedList<T> class, which is a generic class that allows you to create a collection as double linked list. Let’s create an application named GenericLinkedListSample, also available on the CD-ROM, to show the use of the LinkedList<T> class. This application contains a sample user interface form with seven buttons--Create and adds 10 elements, AddFirst, AddLast, RemoveFirst, AddAfter, AddBefore, and RemoveLast, and also contains a ListBox control.

Perform the following steps to create the GenericLinkedListSample application:

+   1. Set the Text property of Form1 to Generic LinkedList Sample in the GenericLinkedListSample application.
+   2. Add a ListBox, a GroupBox, and seven Button controls to the Form1 form.
+   3. Set the Text property of the GroupBox control to Noteworthy Operations and the Text property of button1 to Create and add 10 items, button2 to AddFirst, button3 to AddLast, button4 to RemoveFirst, button5 to AddAfter, button6 to AddBefore, and button7 to RemoveLast.
+   4. Add the code given in Listing 32.8 to the Form1.cs file of the GenericLinkedListSample application: