# 7.3 Different Types of Collections

There are three basic type of collection (List, HashSet and Dictionary) defined in the collections namespace.

| Activity 1 |
| --- |
| Go online to msdn.microsoft.com. This is the website for the Microsoft Developer Network and the contains details of the Application Programmer Interface (API) for the .NET framework (it also contains much more).\ Go online to msdn.microsoft.com. This is the website for the Microsoft Developer Network and the contains details of the Application Programmer Interface (API) for the .NET framework (it also contains much more). | Follow the links for Library (tab near top of page) .NET Development (on left pane) .NET Framework 4 .NET Framework Class Library | At this point you will see all of the namespaces (packages) in the .NET framework on the left with a description of each on the right) | Follow the link for System,Collections and then System.Collections.Generic Look at the class documentation in the main pane and identify any other collections that you may find useful. | Feedback 1 | One of the classes you may have identified is SortedDictionary ... this is just like a dictionary that we will cover one where the elements are automatically sorted for us. We will use a sorted dictionary in the large case study (Chapter 11). | Other collections include LinkedList, Queue, and Stack. Discussions of these are beyond the scope of this but if you have an understanding of Queues, or Linked Lists then it is worth knowing that these have been implemented for you as part of the .NET framework.

# 7.4 Lists

Lists are the most commonly used type of collection – where you might have used an array, a List will provide a more convenient method of handling the data.

Lists are very general-purpose data structures, with each item occupying a specific position. They are in many ways arrays, but are more flexible as they are automatically resized as data is added. They are also much easier to manipulate than arrays as many useful methods have been created to do the bulk of the work for you. Lists items in a particular sequence (though not necessarily sorted into any meaningful order) and duplicate items are permitted.

We will look at the List, HashSet and Dictionary classes, discuss what they do and show some of the more common useful methods that exist.