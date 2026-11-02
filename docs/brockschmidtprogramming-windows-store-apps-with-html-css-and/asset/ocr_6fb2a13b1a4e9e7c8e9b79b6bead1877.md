itself is made up of a <button> with the class win-navigation-backbutton (for the overall control, including pseudo-selectors) and a <span> with the class win-back (that isolates the ring and the arrow character). You can use these to change the coloration of the control:

```
```css
.win-back {
    border-color: rgb(255, 106, 0); /* Circle color */
    color: rgb(255, 106, 0); /* Arrow color */
}

.win-navigation-backbutton:hover .win-back {
    background-color: rgba(255, 106, 0, 0.23);
    border-color: rgb(255, 106, 0);
    color: rgb(255, 106, 0);
}

.win-navigation-backbutton:hover:active .win-back,
.win-navigation-backbutton:active .win-back {
    background-color: rgb(128, 51, 0);
    border-color: rgb(51, 51, 51);
    color: rgb(255, 255, 255);
}
```
```

![](bbox=[0.682, 0.153, 0.735, 0.296])

Note that if you set the background-color for win-navigation-backbutton, you'll set that color for the control's entire rectangle. By default that background is transparent, so you'll typically just style the inner part of the circle, as shown above.

For the DatePicker and TimePicker, refer to styling for the HTML select element along with the ::-ms-value and ::-ms-expand pseudo-elements. I will note that the sample isn't totally comprehensive, so the visuals below highlight the finer points:

+   - win-timepicker and win-datepicker style the whole control (you override defaults)
+   - win-datepicker * style individual parts (display: none will hide that part)
+   - win-*row controls the sub-element for positioning
+   - Style { display: block; float: none } on children for vertical layout

![](bbox=[0.155, 0.607, 0.467, 0.667])

```
```css
.win-datepicker .win-datepicker-year {
    color: blue;
}

.win-datepicker .win-datepicker-date {
    color: green;
}

.win-datepicker .win-datepicker-month {
    color: orange;
}

.win-datepicker .win-datepicker-year::-ms-expand {
    color: red;
}

.win-datepicker .win-order0 {
    background-color: rgb(255, 255, 248);
}

.win-datepicker .win-order1 {
    background-color: rgb(248, 255, 255);
}

.win-datepicker .win-order2 {
    background-color: rgb(248, 255, 255);
}
```
```

![](bbox=[0.157, 0.719, 0.237, 0.788])

```
```css
.win-datepicker[class~="win-datepicker"] {
    display: block;
    float: none;
}
```
```