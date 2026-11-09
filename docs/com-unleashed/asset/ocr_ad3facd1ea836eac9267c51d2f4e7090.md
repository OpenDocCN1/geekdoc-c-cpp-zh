The rest is easy. Just add your code to `Load()` and `Save()`, and the control will persist the desired data.

The second sample object is named `AtlPersistControl2`. (It's in the Chapter03 directory under the AtlPersistControl2 subdirectory.) The full control class that was added is named `PersistClass2`. If you take a look at Listing 4.8, you'll see the salient portions of the PersistClass2.h file. The constructor does not perform the same initialization that I pointed out in the first example. This time around, we'll actually use the data. You can also see the methods that were added. Finally, note the `OnDraw()` method. It uses the `m_TextData` structure to draw to the window.

# **LISTING 4.8**  `PersistClass2.h` (Partial)—Data Structure Initialization, Added Method Overrides, and Altered `OnDraw()` Method

```
public:
    CPersistClass2()
    {
        // Clear the data structure.
        memset( &m_TextData, 0, sizeof( TEXTDATA ) );
        // Initialize with the clock tick count.
        wsprintf( m_TextData.szText, "GetTickCount()=%d",
            GetTickCount() );
        // Set the color.
        m_TextData.Color = RGB( 255, 255, 0 );
    }

typedef struct{
    char szText[400];
    COLORREF Color;
} TEXTDATA;

TEXTDATA m_TextData;

// Other stuff here...

// IPersistClass2
public:
    STDMETHOD(InitNew)(void);
    STDMETHOD(Save)(IStream *pStm, BOOL bClearDirty);
    STDMETHOD(Load)(IStream *pStm);
    STDMETHOD(IsDirty)(void);

    HRESULT OnDraw(ATL_DRAWINFO& di)
    {
        RECT& rc = *(RECT*)di.prcBounds;
        Rectangle(di.hdcDraw, rc.left, rc.top, rc.right, rc.bottom);

        SetTextAlign(di.hdcDraw, TA_CENTER|TA_BASELINE);
```