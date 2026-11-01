```
}
if (!isLoaded)
{
    documentEditTimes[documentName].IsActive = false;
    documentEditTimes[documentName].Document = null;
}
```

For each monitor, a list item is added to the list box that includes the document name and its total edit time:

```
// Add item
this.timerList.Items.Add(string.Format("{0}: {1}", documentName,
    documentEditTimes[documentName].EditTime +
    (documentEditTimes[documentName].IsActive ?
    (DateTime.Now - documentEditTimes[documentName].LastActive) :
    new TimeSpan(0))));
}
```

This completes the code in this example. This example has shown you how to use ribbon and task pane controls and how to maintain task panes in multiple Word documents. It has also illustrated many of the techniques covered earlier in the chapter.

# SUMMARY

In this chapter you have learned how to use VSTO to create managed solutions for Office products.

In the first part of this chapter, you learned about the general structure of VSTO projects and the project types that you can create. You also saw the features that you can use to make VSTO programming easier.

In the next section, you looked, in great depth, at some of the features available in VSTO solutions and you saw how communication with the Office object model is achieved. You also looked at the namespaces and types available in VSTO and learned how to use those types to implement a variety of functionality. Then, you explored some of the code features of VSTO projects and how to use these features to get the effect you want.

After this, you moved on to the more practical side of things. You learned how add-ins are managed in Office applications and how to interact with the Office object model. You also saw how to customize the UI of your applications with ribbon menus, task panes, and action panes.

Finally, you explored an example application that illustrated the UI and interaction techniques that you learned earlier. The example contained a lot of code, but it included useful techniques, including how to manage task panes in multiple Word document windows.