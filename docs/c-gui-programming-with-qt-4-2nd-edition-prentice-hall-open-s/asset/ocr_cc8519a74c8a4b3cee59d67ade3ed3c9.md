```
QString title = fields[0];
QString body = fields[1];
printBox(painter, title, titleFont, Qt::lightGray);
printBox(painter, body, bodyFont, Qt::white);
painter->translate(0, MediumGap);
painter->restore();
```

```
painter->setFont(footerFont);
painter->drawText(painter->window(),
Qt::AlignCenter | Qt::AlignBottom,
QString::number(pageNum));
```

The printPage() function iterates through all the flower guide entries and prints them using two calls to printBox(): one for the title (the flower's name) and one for the body (its description). It also draws the page number centered at the bottom of the page. The page layout is shown schematically in Figure 8.22.

```
void PrintWindow::printBox(QPainter painter, const QString &str,\const QFont &font, const QBrush &brush)
painter->setFont(font);
int boxWidth = painter->window().width();
int textWidth = boxWidth - 2 SmallGap;
int maxHeight = painter->window().height();
QRect textRect = painter->boundingRect(SmallGap, SmallGap,
textWidth, maxHeight, Qt::TextWordWrap, str);
int boxHeight = textRect.height() + 2 * SmallGap;
painter->setPen(QPen(Qt::black, 2.0, Qt::SolidLine);
painter->setBrush(brush);
painter->drawRect(0, 0, boxWidth, boxHeight);
painter->drawText(textRect, Qt::TextWordWrap, str);
painter->translate(0, boxHeight);
```

# Figure 8.22. The flower guide's page layout