```
typedef QVector<Point2D> PointVector;
```

From then on, we can use PointVector as a shorthand for QVector<Point2D>. Notice the new name for the type appears after the old name. The typedef syntax deliberately mimics that of variable declarations.

In Qt, typedefs are used multily for several reasons:

+   - Convenience: Qt declares uint and QWidgetList as typedefs for unsigned int and QList<Widget *> to save a few keystrokes.
- Platform differences: Certain types need different definitions on different platforms. For example, qlonglong is defined as __int64 on Windows and as long long on other platforms.
- Compatibility: The QIcon class from Qt 3 was renamed QIcon in Qt 4. To help Qt 3 users port their applications to Qt 4, QsetIcon is provided as a typedef when Qt 3 compatibility is enabled.

# Type Conversions

C++ provides several syntaxes for casting values from one type to another. The traditional syntax, inherited from C, involves putting the resulting type in parentheses before the convert:

```
const double Pi = 3.14159265359;
int x = (int)(Pi * 100);
std::cout << x << " equals 314" << std::endl;
```

This syntax is very powerful. It can be used to change the types of pointers, to remove const, and much more. For example:

```
short j = 0x1234;
if (*char*)&j == 0x12
std::cout << "The byte order is big-endian" << std::endl;
```

In the preceding example, we cast a short * to a char * and use the unary operator to access the byte at the given memory location. On big-endian systems, that byte is 0x12; on little-endian systems, it is 0x34. Since pointers and references are represented the same way, it should come as no surprise the preceding code can be rewritten using a reference cast:

```
short j = 0x1234;
```