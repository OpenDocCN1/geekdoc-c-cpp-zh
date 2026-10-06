QWindowsVistaStyle and QMacStyle use this technique to animate default buttons.

```
int BronzeStyle::styleHint(StyleHint which, const QStyleOption option,
 QWidget* widget,
 QHintReturn *returnData) const
```

```
{
    switch (which) {
        case SH_DialogButtonLayout:
            return int(DialogButton::MacLayout);
        case SH_EtchDisabledText:
            return int(true);
        case SH_DialogButtonBox_ButtonsHaveIcons:
            return int(true);
        case SH_UnderlineShortcut:
            return int(false);
        default:
            return QWindowsStyle::styleHint(which, widget,
returnData);
    }
}
```

The styleHint() function returns some hints about the look and feel provided by the style. For example, we return MacLayout for SH_DialogButtonLayout to signify that we want QDialogButtonBox to follow the Mac OS X guidelines, with OK to the right of Cancel. The return type of styleHint() is int. For the few style hints that styleHint() provides a pointer to a QHintReturn object that can be used.

```
int BronzeStyle::pixelMetric(PixelMetric which,
 const QStyleOption *option,
 const QWidget *widget) const
```

```
{
    switch (which) {
        case PM_ButtonDefaultIndicator:
            return 0;
        case PM_IndicatorWidth:
        case PM_IndicatorHeight:
            return 16;
        case PM_CheckBoxLabelSpacing:
            return 8;
        case PM_DefaultFrameWidth:
            return 2;
        default:
            return QWindowsStyle::pixelMetric(which, option, widget);
    }
```