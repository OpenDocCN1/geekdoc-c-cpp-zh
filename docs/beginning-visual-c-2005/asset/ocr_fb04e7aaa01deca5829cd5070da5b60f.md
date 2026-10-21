# Chapter 17

```
m_pSelected->Draw(&aDC,m_pSelected);  // Draw highlighted

return;
}

// ...otherwise, use this method
aDC.SetROP2(R2_NOTXORPEN);
m_pSelected->Draw(&aDC,m_pSelected);    // Draw the element to erase it
m_pSelected->Move(Distance);            // Now move the element
m_pSelected->Draw(&aDC,m_pSelected);    // Draw the moved element
}
```

You can see that the code for invalidating the rectangles that you must use for moving the text is much less elegant than the ROP code that you use for all the other elements. It works, though, as you’ll see for yourself if you make this modification and then build and run the application. If you would like to try the typeid() mechanism for testing the type, just change the condition in the if statement and add the #include directive for <typeinfo> to SketcherView.cpp.

# Printing a Document

Now take a look at printing the document. You already have a basic printing capability implemented in the Sketcher program, courtesy of the Application wizard and the framework. The File > Print, File > Print Setup, and File > Print Preview menu items all work. Selecting the File > Print Preview menu item displays a window showing the current Sketcher document on a page, as shown in Figure 17-4.

![](bbox=[0.23, 0.53, 0.71, 0.77])

Figure 17-4

Whatever is in the current document is placed on a single sheet of paper at the current view scale. If the document’s extent is beyond the boundary of the paper, the section of the document off the paper won’t be printed. If you select the Print button, this page is sent to your printer.