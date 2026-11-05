A sample run of the application is shown in Figure 13–9.

![](bbox=[0.186, 0.146, 0.912, 0.491])

**FIGURE 13–9**  Output from the FileAccessApp application

> **NOTE**  One of the properties of the ListBox objects is `Sorted`. By default, it is set to `false`; however, you can change that and have the entries in the list box in sort order—even if they are not sorted in the file. For this application, the `Sorted` property was changed to `true`.

In Example 13–5, the try...catch block was enclosed inside a selection statement. The if statement was used to check to see if the file existed. When an invalid path was specified, an exception was not thrown and the try...catch block was skipped. Examine the while statement that appears in Example 13–5.

```
while ((inValue = inFile.ReadLine()) != null)
```

The ReadLine() method is used with the infile object to retrieve one line of text from the file. The line is stored in the inValue variable. The while statement tests each access from the file and continues looping until inValue == null, indicating that all the lines have been read.

# Adding a Using Statement

The using keyword has two major uses. Previously, you added a using clause to your program statements to import types defined in namespaces. By doing this, you were able to avoid fully qualifying references to types. For example, by adding