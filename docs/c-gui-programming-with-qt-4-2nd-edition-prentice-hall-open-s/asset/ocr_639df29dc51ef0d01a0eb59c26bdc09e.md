```
buttonRect.setWidth(buttonRect.width() + 1);

QStyleOption button(*option);
painter->save();npainter->setClipRect(buttonRect, Qt::IntersectClip);
if (!(option->activeSubControls & which))
	buttonOpt.state &= ~(State_MouseOver | State_On | State_Sunker)
	drawBronzeBevel(&buttonOpt, painter);

QStyleOption arrowOpt(buttonOpt);
arrowOpt.rect = subControlRect(CC_SpinBox, option, which)
	adjust(+3, +3, -3, -3);
	if (arrowOpt.rect.isValid())
	drawPrimitive(arrow, &arrowOpt, painter);
painter->restore();
}
```

The drawBronzeSpinButton() function draws the up or down button of a spin box, depending on which is SC_SpinBoxDown or SC_SpinBoxUp. We start by setting up the arrow to draw on the button (a left or a right arrow) and draw the arrow in the rectangle we draw.

If which is SC_SpinBoxDown (or which is SC_SpinBoxUp and the layout direction is right-to-left, we use a left arrow (PE_IndicatorArrowLeft) and we draw the button in the left half of the spin box's rectangle; we use a right arrow and draw the button in the right half.

To draw the button, we call drawBronzeBevel() with a QStyleOption that correctly reflects the state of the spin box we draw. For example, if the mouse is hovering over the spin box but not over the spin box which, we clear the State_MouseOver, State_On, and State_Sunken flags from the QStyleOption's state. It is necessary to ensure that the two spin buttons behave independently of each other.

By performing any, we use setClipRect() to set the clipping rectangle on the QPainter. This is because we want to draw only the left or right half of a bevel, not the entire button bevel.

Finally, at the end, we draw the arrow by calling drawPrimitive(). The QStyleOption used to draw the arrow is set up with a rectangle that corresponds to the spin box button's rectangle (SC_SpinBoxUp or SC_SpinBoxDown) but is a bit smaller, to obtain a smaller arrow.