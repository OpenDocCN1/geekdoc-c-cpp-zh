For this, for example, we choose WindowsStyle, the classic Windows style. Even though the Bronze style doesn't look like the Windows style, there is a large body of code in WindowsStyle QCommonStyle that can be reused to implement just any style we can imagine. This is why QMacStyle is derived from WindowsStyle even though they look very different.

BronzeStyle reimplements several public functions declared by polish() and unpolish() functions when the style is installed or uninstalled. They make it possible to tweak the widgets or the palette. The other public functions are either query functions (styleHint(), pixelMetric(), subControlRect()) or functions that draw a graphical element (drawPrimitive(), drawComplexControl()).

BronzeStyle also provides a public slot standardIconImplementation(). This slot is declared by Qt introspection and is invoked when necessary as though it had been a virtual function. Qt sometimes uses this idiom to add functions that should have been virtual without binary compatibility with Qt 4 releases. It is expected that Qt 5 will replace the standardIconImplementation() slot with a standardIcon() virtual function.

The BronzeStyle also declares a few private functions. These will be explained after we have covered the functions.

```
void BronzeStyle::polish(QPalette& palette)
{
    QPixmap backgroundImage(":/images/background.png");
    QColor bronze(207, 155, 95);
    QColor veryLightBlue(239, 239, 247);
    QColor lightBlue(223, 223, 239);
    QColor darkBlue(95, 95, 191);

    palette = QPalette(bronze);
    palette.setBrush(QPalette::Window, backgroundImage);
    palette.setBrush(QPalette::BrightText, Qt::white);
    palette.setBrush(QPalette::Base, veryLightBlue);
    palette.setBrush(QPalette::AlternateBase, lightBlue);
    palette.setBrush(QPalette::Highlight, darkBlue);
    palette.setBrush(QPalette::Disabled, QPalette::Highlight,
    Qt::darkGray);
}
```

One of the outstanding characteristics of the Bronze style is its color scheme. No matter what colors the user has set on their window system, the Bronze style has a bronze appearance. A custom style's color scheme can be set up in one of