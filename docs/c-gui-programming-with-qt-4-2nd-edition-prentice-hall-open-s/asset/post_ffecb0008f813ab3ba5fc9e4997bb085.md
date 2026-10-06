
# 5. Creating Custom Widgets

![](img/5a524abdf0b0d58fa99d30abb4463611_172_0.png)

- Customizing Qt Widgets
- Subclassing QWidget
- Integrating Custom Widgets with Qt Designer
- Double Buffering

This chapter explains how to develop existing custom widgets using Qt. Custom widgets can be created by subclassing an existing Qt widget or by subclassing QWidget directly. We will demonstrate both approaches, and we will also see how to integrate a custom widget with Qt Designer so that it can be used just like a built-in Qt widget. We will round off the chapter by presenting a custom widget that uses double buffering, a powerful technique for high-speed drawing.

## Customizing Qt Widgets

In some cases, we find that a Qt widget requires more customization than is possible by setting its properties in Qt Designer or by calling its functions. A simple and direct solution is to subclass the relevant widget class and adapt it to suit our needs.

In this section, we will develop the hexadecimal spin box shown in Figure 5.1, to demonstrate how this works. QSpinBox supports only decimal integers, but by subclassing it's quite easy to make it accept and display hexadecimal values.

## Figure 5.1. The HexSpinBox widget

![](img/5a524abdf0b0d58fa99d30abb4463611_172_1.png)

```cpp
#ifndef HEXSPINBOX_H
#define HEXSPINBOX_H

#include <QSpinBox>

class QRegExpValidator;

class HexSpinBox : public QSpinBox
{
    Q_OBJECT
public:
    HexSpinBox(QWidget parent = nullptr);

protected:
  QValidator::State validate(QString &text, int &pos) const;
  int valueFromText(const QString &text) const;
  QString textFromValue(int value) const;

private:
  QRegExpValidator validator;
};

#endif
```

HexSpinBox inherits its functionality from QSpinBox. It provides a typical constructor and reimplements three virtual functions from QSpinBox.

```cpp
#include <QtGui>
#include "hexspin.h"
```

```cpp
HexSpinBox::HexSpinBox(QWidget *parent)
    : QSpinBox(parent)
{
  setRange(0, 255);
  validator = new QRegExpValidator(QRegExp("[0-9A-Fa-f]{1,8}"), this);
}
```

We set the default range to be from 0 to 255 (0x00 to 0xFF), which is more appropriate for a spin box QSpinBox's default of 0 to 99.

The user can modify a spin box's current value by clicking its up and down arrows or by typing a value in the spin box's line editor. In the latter case, we must restrict the user's input to legitimate hexadecimal numbers. To achieve this, we use a QRegExpValidator that accepts one and eight characters, all of which must be in the set {'0', '1', ..., '9', 'A', 'B', ..., 'F', 'a', 'b', ..., 'f'}.

```cpp
QValidator::State HexSpinBox::validate(QString &text, int &pos) const
{
  return validator->validate(text, pos);
}
```

Function is called by QSpinBox to see if the text entered so far is valid. There are three possible results: Invalid (the text doesn't match the regular expression), Acceptable (the text is a valid value), and Intermediate (the RegExpValidator has a suitable validate() function, so we may simply return the result of calling it). In theory, we should return Invalid or Intermediate for values that lie outside the spin box's range, QSpinBox is used to detect changes without any help.

```cpp
QString HexSpinBox::textFromValue(int value) const {
    return QString::number(value, 16).toUpperCase();
}
```

The textFromValue() function converts an integer value to a string. QSpinBox calls it to update the editor part of the spin box when the user presses the spin box's up or down arrows. We use the static function QString::number() with a second argument of 16 to convert the value to hexadecimal, and call QString::toUpperCase() on the result to make it uppercase.

```cpp
int HexSpinBox::valueFromText(const QString &text) const {
    bool ok;
    return text.toInt(&ok, 16);
}
```

The valueFromText() function performs the reverse conversion, from a string to an integer value. It is called by QSpinBox when the user types a value into the editor part of the spin box and presses Enter. The QString::toInt() function to convert the current text to an integer value, using base 16. If the string is not valid hexadecimal, ok is set to false and toInt() returns 0. Here, we don't have to consider this possibility because the validator permits only hexadecimal strings to be entered. Instead of passing the address of a dummy variable (ok), we could pass a null pointer as the first argument to toInt().

We have now finished the hexadecimal spin box. Customizing Qt widgets follows the same pattern: Pick a suitable Qt widget, subclass it, and reimplement some virtual functions to change its behavior. If all we want to customize an existing widget's look and feel, we can apply a style sheet or implement a custom style instead of subclassing the widget, as explained in Chapter 19.
