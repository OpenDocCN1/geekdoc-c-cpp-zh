# 9

# File Handling

# WHAT YOU WILL LEARN IN THIS CHAPTER:

+   - Where your applications are stored on the iPad
+   - The various folders within your `Applications` folder
+   - How to read and write to files in the `Documents` and `tmp` folders
+   - How to use a property to store structured data
+   - How to programmatically retrieve values stored in a property list
+   - How to modify the values retrieved from a property list and save the changes to a file
+   - How to copy bundled resources to the application's folder during runtime

All the applications you have developed up to this point are pretty straightforward — the application starts, performs something interesting, and ends. In Chapter 8, you saw how you can make use of the application settings feature to save the preferences of your application to a central location managed by the Settings application. Sometimes, however, you simply need to save some data to your application’s folder for use later. For example, rather than keep files you download from a remote server in memory, a more effective and memory efficient method is to save them in a file so that you can use them later (even after the application has shut down and restarted).

In this chapter, you learn more about how you can persist data in your application so that you can use it later. You learn the two available approaches: saving the data as files and as a property list. You also learn how to bundle resources such as text files and database files with your application so that when the application is installed on the user’s device, the resources can be copied onto the local storage of the device and be used from there.