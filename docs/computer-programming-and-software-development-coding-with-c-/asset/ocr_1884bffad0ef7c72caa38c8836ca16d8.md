# Chapter 10 How to Create Generic Interface

In this demonstration, you will learn how to create a generic interface. Here, I've opened the Program.cs file of the StorageApp. Previously, you have created the SqlRepository class, but it does not work with these methods, as these methods have a ListRepository parameter. Now let's introduce a generic IRepository interface so that these methods work not only with list repositories, but also with SQL repositories. To do this, let's open here the SqlRepository class. First, let me put the cursor on the usings, and let's press Ctrl+dot to remove unnecessary usings. Now, let's put the cursor on the SqlRepository class name, and let's press Ctrl+dot, and you can see Visual Studio suggests here to extract an interface.

![](bbox=[0.121, 0.536, 0.912, 0.812])

Let's press Enter to select this option. In this dialog, let's call the new interface just IRepository, and I want to create it in the new file