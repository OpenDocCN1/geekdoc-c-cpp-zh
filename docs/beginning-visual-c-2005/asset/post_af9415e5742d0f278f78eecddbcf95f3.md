
# Chapter 17

```
// set the last page number as the total number of pages
pInfo->SetMinPage(1);
pInfo->SetMaxPage((static_cast<CPrintData*>(pInfo->m_lpUserData))->m_nWidths * (static_cast<CPrintData*>(pInfo->m_lpUserData))->m_nLengths);
```

```
return DoPreparePrinting(pInfo);
}
```

You first create a CPrintData object on the heap and store its address in the pointer m_lpUserData in the CPrintInfo object passed to the function via the pointer pInfo. After getting a pointer to the document, you get the rectangle enclosing all of the elements in the document by calling the function GetDocExtent() that you added to the document class earlier in this chapter. You then store the corner of this rectangle in the m_DocRefPoint member of the CPrintData object and put the name of the file that contains the document in m_DocTitle.

Referencing the CPrintData object through the pointer in the CPrintInfo object is rather cumbersome. You get to the pointer with the expression pInfo->m_lpUserData, but because the pointer is of type void, you must add a cast to type CPrintData* to get to the m_DocRefPoint member of the object. The full expression to access the reference point for the document is:

```
(static_cast<CPrintData*>(pInfo->m_lpUserData))->m_DocRefPoint
```

You have to use this approach for all references to members of the CPrintData object, so any expressions using them are festooned with this notation. If you put the data in the view class, you only need to use the name of the data member. Don’t forget to add an #include directive for PrintData.h to the SketcherView.cpp file.

The next two lines of code calculate the number of pages across the width of the document, and the number of pages required to cover the length. The number of pages to cover the width is computed by dividing the width of the document by the width of the print area of a page, which is 600 units or 6 inches, and rounding up to the next highest integer using the ceil() library function that is defined in the <cmath> header. An #include for this header file also needs to be added to SketcherView.cpp. For example, ceil(2.1) returns 3.0, ceil(2.9) also returns 3.0, and ceil(-2.1) returns -2.0. A similar calculation to that for the number of pages across the width of a document produces the number to cover the length. The product of these two values is the total number of pages to be printed, and this is the value that you’ll supply for the maximum page number.

## Cleaning Up After Printing

Because you created the CPrintData object on the heap, you must ensure that it’s deleted when you’re done with it. You do this by adding code to the OnEndPrinting() function:

```
void CSketcherView::OnEndPrinting(CDC* /*pDC*/, CPrintInfo* pInfo)
{
```

```
// Delete our print data object
delete static_cast<CPrintData*>(pInfo->m_lpUserData);
```

```
}
```

That’s all that’s necessary for this function in the Sketcher program, but in some cases you’ll need to do more. Your one-time final cleanup should be done here. Make sure that you remove the comment delimiters (/* */) from the second parameter name; otherwise, your function won’t compile. The default implementation comments out the parameter names because you may not need to refer to them in your code. Because you use the pInfo parameter, you must uncomment it; otherwise, the compiler reports it as undefined.

You don’t need to add anything to the OnBeginPrinting() function in the Sketcher program, but you’d need to add code to allocate any GDI resources, such as pens, if they were required throughout the printing process. You would then delete these as part of the clean up process in OnEndPrinting().

## Preparing the Device Context

At the moment, the Sketcher program calls OnPrepareDC(), which sets up the mapping mode as MM_ANISOTROPIC to take account of the scaling factor. You must make some additional changes so that the device context is properly prepared in the case of printing:

```
void CSketcherView::OnPrepareDC(CDC* pDC, CPrintInfo* pInfo)
{
    int Scale = m_Scale;                     // Store the scale locally
    if(pDC->IsPrinting())
        Scale = 1;                           // If we are printing, set scale to 1

    CScrollView::OnPrepareDC(pDC, pInfo);
    CSketcherDoc* pDoc = GetDocument();
    pDC->SetMapMode(MM_ANISOTROPIC);         // Set the map mode
    CSize DocSize = pDoc->GetDocSize();       // Get the document size

    // y extent must be negative because we want MM_LOENGLISH
    DocSize.cy = -DocSize.cy;                // Change sign of y
    pDC->SetWindowExt(DocSize);              // Now set the window extent

    // Get the number of pixels per inch in x and y
    int xLogPixels = pDC->GetDeviceCaps(LOGPIXELSX);
    int yLogPixels = pDC->GetDeviceCaps(LOGPIXELSY);

    // Calculate the viewport extent in x and y
    long xExtent = static_cast<long>(DocSize.cx)*Scale*xLogPixels/100L;
    long yExtent = static_cast<long>(DocSize.cy)*Scale*yLogPixels/100L;

    pDC->SetViewportExt(static_cast<int>(xExtent),
                        static_cast<int>(-yExtent)); // Set viewport extent
}
```

This function is called by the framework for output to the printer as well as to the screen. You should make sure that a scale of 1 is used to set the mapping from logical coordinates to device coordinates when you’re printing. If you left everything as it was, the output would be at the current view scale, but you’d need to take account of the scale when calculating how many pages you needed, and how you set the origin for each page.

You can determine whether you have a printer device context or not by calling the IsPrinting() member of the current CDC object, which returns TRUE if you are printing. All you need to do when you have
a printer device context is to set the scale to 1. Of course, you must change the statements lower down which use the scale value, so that they use the local variable Scale rather than the m_Scale member of the view. The values returned by the calls to GetDeviceCaps() with the arguments LOGPIXELSX and LOGPIXELSY return the number of logical points per inch in the x and y directions for your printer when you’re printing, and the equivalent values for your display when you’re drawing to the screen, so this automatically adapts the viewport extent to suit the device to which you’re sending the output.

## Printing the Document

You can write the data to the printer device context in the OnPrint() function. This is called once for each page to be printed. You need to add an override for this function to CSketcherView, using Properties window for the class. Select OnPrint from the list of overrides and then click <Add> OnPrint in the right column.

You can obtain the page number of the current page from the m_nCurPage member of the CPrintInfo object and use this value to work out the coordinates of the position in the document that corresponds to the upper-left corner of the current page. The way to do this is best understood using an example, so imagine that you are printing page seven of an eight-page document, as illustrated in Figure 17-7.

![](img/2359b0c604600c58fba3539c738a356e_935_0.png)

Figure 17-7

You can get an index to the horizontal position of the page by decrementing the page number by 1 and taking the remainder after dividing by the number of page widths required for the width of the printed area of the document. Multiplying the result by 600 produces the x coordinate of the upper-left corner of the page, relative to the upper-left corner of the rectangle enclosing the elements in the document. Similarly, you can determine the index to the vertical position of the document by dividing the current page number reduced by 1 by the number of page widths required for the horizontal width of the
document. By multiplying the remainder by 900, you get the relative y coordinate of the upper-left corner of the page. You can express this in two statements as follows:

```
int xOrg = (static_cast<CPrintData*>(pInfo->m_lpUserData))->m_DocRefPoint.x +
    600*((pInfo->m_nCurPage - 1)%
    ((static_cast <CPrintData*>(pInfo->m_lpUserData))->m_nWidths));
int yOrg = (static_cast<CPrintData*>(pInfo->m_lpUserData))->m_DocRefPoint.y -
    900*((pInfo->m_nCurPage - 1) /
    ((static_cast <CPrintData*>(pInfo->m_lpUserData))->m_nWidths));
```

The statements look complicated, but that’s mostly because of the need to access the information stored in the CPrintData object through the pointer in the CPrintInfo object.

It would be nice to print the file name of the document at the top of each page, but you want to be sure you don’t print the document data over the file name. You also want to center the printed area on the page. You can do this by moving the origin of the coordinate system in the printer device context after you have printed the file name. This is illustrated in Figure 17-8.

![](img/2359b0c604600c58fba3539c738a356e_936_0.png)

Figure 17-8
