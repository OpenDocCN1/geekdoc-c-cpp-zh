# CHAPTER 5 CONTENT CONTROLS

(continued)

| VALUE | POSITION IS RELATIVE TO: |
| MousePoint | The mouse's position. If the pop-up won't fit, it is extended from an axis defined by Horizontaloffset or VerticalOffset |
| Left | Left edge of PlacementTarget |
| Top | Top edge of PlacementTarget |
| Custom | A position specified by a CustomPopupPlacementCallback |

The PopupPlacement example shown in Figure 5-10 demonstrates the most common Placement values. All pop-ups have their PlacementTarget values set to the Image control.

![](bbox=[0.095, 0.351, 0.335, 0.477])

FIGURE 5-10

> PUSHY POP-UPS
Pop-ups float over the application. If you move the application, they remain where they were originally positioned and do not move with the application.
In fact, pop-ups tend to float above all other applications, too. If you switch to another program, the pop-ups remain visible floating over the new program.

By default, a pop-up remains invisible until its IsOpen property is set to False. If you set the control's StayOpen property to False, the Popup automatically captures the mouse and hides when a mouse event occurs outside the Popup.

The final Popup property mentioned here is PopupAnimation. You can set this property to None (the pop-up simply appears), Fade (the pop-up fades in and out), Scroll (the pop-up scrolls from its upper-left corner), and Slide (the pop-up slides down from the top or from the bottom if it won't fit sliding down). To use any of these values other than None, you must set the control's AllowsTransparency property to True.