# 5. Creating Custom Widgets

![](bbox=[0.012, 0.046, 0.185, 0.142])

+   - Customizing Qt Widgets
- Subclassing QWidget
- Integrating Custom Widgets with Qt Designer
- Double Buffering

This chapter explains how to develop existing custom widgets using Qt. Custom widgets can be created by subclassing an existing Qt widget or by subclassing QWidget directly. We will demonstrate both approaches, and we will also see to integrate a custom widget with Qt Designer so that it can be used just like a built-in in Qt widget. We will round off the chapter by presenting a custom widget that uses double buffering, a powerful technique for high-speed drawing.

# Customizing Qt Widgets

In some cases, we find that a Qt widget requires more customization than is possible by setting its properties in Qt Designer or by calling its functions. A simple and direct solution is to subclass the relevant widget class and adapt it to suit our needs.

In this section, we will develop the hexadecimal spin box shown in Figure 5.1, to demonstrate how this works. QSpinBox supports only decimal integers, but by subclassing it's quite easy to accept and display hexadecimal values.

# Figure 5.1. The HexSpinBox widget

![](bbox=[0.012, 0.733, 0.118, 0.762])

```
#ifndef HEXSPINBOX_H
#define HEXSPINBOX_H

#include <QSpinBox>

class QRegExpValidator;

class HexSpinBox : public QSpinBox
{
    Q_OBJECT
```