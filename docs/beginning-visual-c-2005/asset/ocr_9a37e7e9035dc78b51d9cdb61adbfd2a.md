# Chapter 14

the cursor position when the left mouse button was pressed. The UINT type is defined in the Windows API and corresponds to a 32-bit unsigned integer.

The value of nFlags that is passed to the function can be any combination of the following symbolic values:

| Flag | Description |
|------|-------------|
| MK_CONTROL | Corresponds to the Ctrl key being pressed. |
| MK_LBUTTON | Corresponds to the left mouse button being down. |
| MK_MBUTTON | Corresponds to the middle mouse button being down. |
| MK_RBUTTON | Corresponds to the right mouse button being down. |
| MK_SHIFT | Corresponds to the Shift key being pressed. |

Being able to detect if a key is down in the message handler enables you to support different actions for the message depending on what else you find. The value of nFlags may contain more than one of these indicators, each of which corresponds to a particular bit in the word, so you can test for a particular key using the bitwise AND operator. For example, to test for the Ctrl key being pressed, you could write:

```
if(nFlags & MK_CONTROL)
    // Do something...
```

The expression nFlags & MK_CONTROL will only have the value TRUE if the nFlags variable has the bit defined by MK_CONTROL set. In this way, you can have different actions when the left mouse button is pressed, depending on whether or not the Ctrl key is also pressed. You use the bitwise AND operator here, so corresponding bits are ANDed together. Don’t confuse this with the logical AND, &&, which would not do what you want here.

The arguments passed to the other two message handlers are the same as those for the OnLButtonDown() function; the code generated for them is:

```
void CSketcherView::OnLButtonUp(UINT nFlags, CPoint point)
{
    // TODO: Add your message handler code here and/or call default

    CView::OnLButtonUp(nFlags, point);
}
```

```
void CSketcherView::OnMouseMove(UINT nFlags, CPoint point)
{
    // TODO: Add your message handler code here and/or call default

    CView::OnMouseMove(nFlags, point);
}
```

Apart from the function names, the skeleton code is the same for each.