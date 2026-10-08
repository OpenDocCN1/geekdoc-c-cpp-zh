# Chapter 15 Graphical User Interfaces with Windows Forms: Part 2

| properties | Description |
| --- | --- |
| ShowUpDown | Indicates whether the control displays up down Buttons. Helpful when the DateTimePicker is used to select a time—the Buttons can be used to increase or decrease hour, minute and second. |
| Value | The data selected by the user. |
| Common DateTimePicker Event | Generated when the value property changes, including when the user selects a new date or time. |

Fig. 15.10 | DateTimePicker properties and an event. (Part 2 of 2.)

15.11 demonstrates a DateTimePicker to select an item's drop-off time. Many companies use such functionality—online retailers typically specify the day a package is sent out and the estimated time that it will arrive at your home. The user selects a drop-off day

```
// Fig. 15.11: DateTimePicker.cs
// Using a DateTimePicker to select a drop-off time.
using System;
using System.Windows.Forms;

namespace DateTimePickerTest
{
    // Form lets user select a drop-off day using a DateTimePicker
    // and displays an estimated delivery date
    public partial class DateTimePickerForm : Form
    {
        // constructor
        public DateTimePickerForm()
        {
            InitializeComponent();
        }

        private void dropOffDatePicker_ValueChanged(
            DateTime dropOff = dropOffDatePicker.Value;
            // add extra time when items are dropped off Sunday
            if (dropOff.DayOfWeek == DayWeek.Friday ||
                dropOff.DayOfWeek == DayWeek.Saturday ||
                dropOff.DayOfWeek == DayWeek.Sunday)
            {
}
}
```

Fig. 15.11 | Using a DateTimePicker to select a drop-off time. (Part I of 2.)