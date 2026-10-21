# Chapter 15

```
OnPrepareDC(&aDC);            // Get origin adjusted

// Get the enclosing rectangle and convert to client coordinates
CRect aRect=((CElement*)pHint)->GetBoundRect();
aDC.LPtoDP(aRect);
InvalidateRect(aRect);        // Get the area redrawn
}
```

```
else
    InvalidateRect(0);          // Invalidate the client area
}
```

The modification here creates a CClientDC object and uses the LPtoDP() function member to convert the rectangle for the area that’s to be redrawn to client coordinates.

If you now compile and execute Sketcher with the modifications I have discussed and are lucky enough not to have introduced any typos, it will work correctly, regardless of the scroller position.

# Using MM_LOENGLISH Mapping Mode

Now look into what you need to do to use the MM_LOENGLISH mapping mode. This provides drawings in logical units of 0.01 inches, and also ensures that the drawing size is consistent on displays at different resolutions. This makes the application much more satisfactory from the users’ point of view.

You can set the mapping mode in the call to SetScrollSizes() made from the OnInitialUpdate() function in the view class. You also need to specify the total drawing area, so, if you define it as 3000 by 3000, this provides a drawing area of 30 inches by 30 inches, which should be adequate. The default scroll distances for a line and a page is satisfactory, so you don’t need to specify those. You can use Class View to get to the OnInitialUpdate() function and then change it to the following:

```
void CSketcherView::OnInitialUpdate(void)
{
    CScrollView::OnInitialUpdate();
```

```
// Define document size as 30x30ins in MM_LOENGLISH
CSize DocSize(3000,3000);

// Set mapping mode and document size.
SetScrollSizes(MM_LOENGLISH, DocSize);
```

```
}
```

You just alter the arguments in the call to SetScrollSizes() for the mapping mode and document the size that you want. That’s all that’s necessary to enable the view to work in MM_LOENGLISH, but you still need to fix how you deal with rectangles.

Note that you are not limited to setting the mapping mode once and for all. You can change the mapping mode in a device context at any time and draw different parts of the image to be displayed using different mapping modes. A function SetMapMode() is used to do this, but I won’t be going into this any further here. You can get your application working just using MM_LOENGLISH. Whenever you create a CClientDC object for the view and call OnPrepareDC(), the device context that it owns has the mapping mode you’ve set in the OnInitialUpdate() function.