in the operating system and window system macros, there is also a set of compiler macros. For example, Q_CC_MSVC if the compiler is Microsoft C++. This can be useful for working around compiler bugs.

Several of Qt's GUI-related classes provide platform-specific functions that return low-level handles to the underlying object. These are listed in Figure 23.2.

# Figure 23.2. Platform-specific functions to access low-level handles

| Mac OS X |
|---||
| ATSFormatRef | QFont::handle() |
| CGImageRef | Qpixmap::macCGHandle() |
| GWPtr | Qpixmap::macQDAlphaHandle() |
| GWPtr | Qpixmap::macQDHandle() |
| RgnHandle | QRegion::handle() |
| HIVViewRef | QWidget::winId() |

| Windows |
|---||
| HCURSOR | Cursor::handle() |
| HDC | QPaintEngine::getDC() |
| HDC | QPrintEngine::getPrinterDC() |
| HFONT | QFont::handle() |
| HPALETTE | QColormap::hPal() |
| HRGN | QRegion::handle() |
| HWND | QWidget::winId() |

| X11 |
|---||
| Cursor | Cursor::handle() |
| Font | QFont::handle() |
| Picture | Qpixmap::x11PictureHandle() |
| Picture | QWidget::x11PictureHandle() |
| Pixmap | Qpixmap::handle() |
| QX11Info | Qpixmap::x11Info() |