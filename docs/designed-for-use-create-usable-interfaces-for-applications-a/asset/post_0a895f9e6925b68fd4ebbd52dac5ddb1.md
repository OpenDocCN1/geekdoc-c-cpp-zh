
![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_135_0.png)

## Figure 13.1: Undoing in BusyCal

You have to come up with your own design, preferably something that feels “natural.” But in real life, you can’t turn back time and revert to the way things were a few seconds ago. So, how do you present that concept in a natural user interface?

Unfortunately, there is no simple, obvious solution to the problem of designing “natural” user interfaces, but there are some ideas you can follow:

- If possible, copy real-world behavior. Have the computer respond immediately and behave in a way that the user will recognize and understand. That way, people can apply real-world knowledge to virtual systems.
- Copy what popular applications are doing. Chances are that your users have already seen these other applications and are familiar with their approach.
- Implement interactive prototypes of different ideas, and do usability tests to see how people react to them.

Until NUIs become more popular, we will have to live with a lack of commonly accepted user interface conventions. This makes our job harder, but fortunately, it also makes it more interesting.

## Takeaway Points

- Allow direct manipulation whenever possible.
- Give immediate, live feedback to any user action.
- Use gestures that don't manipulate objects but instead invoke commands only as shortcuts rather than as primary interactions.
- Make sure people don't have to learn complex gestures.
- Make sure people don't have to make precise gestures; be liberal in accepting user input, but allow them to undo false input.
- Hardware that runs natural user interfaces is especially prone to interpreting unintended user actions as input. Whenever possible, prevent accidental input, and provide fallback solutions for when it does happen.
- Follow what nature does.
- Follow what popular applications do.
- Regularly test interactive prototypes of your user interface with actual people.

## Further Reading

Dan Saffer's *Designing Gestural Interfaces* [Saf08] covers some of the things mentioned in this chapter and many additional topics. Josh Clark talks about gestures (among many other things) in his excellent book *Tapworthy* [Cla10].

Fred Beecher lists a number of useful guidelines for designing natural user interfaces.⁶

## Who’s Fitts?

Fitts’s law is named after its discoverer, Paul Fitts, a psychologist at Ohio State University and later at the University of Michigan.

The law’s name is sometimes written as Fitts’ law, dropping the possessive s, but “Fitts’s law” seems to be the form most commonly used by reputable sources, so I’m going with that version in my book. Please don’t send me mail complaining about it. But here’s my pledge to you: if you manage to change the Wikipedia article and make the change stick, I’ll change it in the book, too.

This idea seems pretty straightforward, and indeed, a number of studies have shown that it is correct.¹ The relevant part of the formula used to calculate the time it takes a user to achieve a task is the index of difficulty (ID), which basically measures how difficult it is to hit a target. This part of the formula reads as follows:

ID = log₂( Distance to target / Width of target in direction of motion +1 )

Since the formula for the ID is logarithmic, even small changes in size can result in comparatively big changes in difficulty if the target is small to begin with. For larger targets, small changes have little effect.

Although the law itself seems obvious enough, some of its effects may not be. Let’s look at a few.

### 14.1 Screen Edges Have Infinite Size

If you think about it, an interface element at the very edge of your screen is essentially infinite in size if you’re trying to hit it with a mouse. No matter how far in the direction of the screen edge you move your mouse, it will never leave the screen and always remain on the target. Thus, it makes sense to put important elements at the very edge of the screen. Hitting such elements is much easier because people can just slam the mouse toward the edge, and it will stop inside the target on its own.

1. You can find references to some of the research on this topic here: http://www.yorku.ca/mack/RN-Fitts_bib.htm.

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_139_0.png)

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_139_1.png)

THIS TARGET TAKES LONGER TO HIT...

...THAN THIS TARGET

Corners are especially valuable, because they have two infinite edges.

In most cases, this same effect does not apply to touch screens, unfortunately. Touching elements closer to the touch screen's edge is not easier than touching elements elsewhere. The areas the user can most easily reach depend on how she holds the device instead.

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_139_2.png)

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_139_3.png)

IF YOU HOLD YOUR IPAD LIKE THIS...

...ONLY PARTS OF YOUR SCREEN CAN EASILY BE REACHED.

Of course, when the user is dragging things, the touch screen's edge becomes an easier target again, because it's not possible to drag things outside of the screen.

### 14.2 Radial Context Menus Decrease Average Distance

As mentioned, corners are especially easy to hit, because they have two infinite edges. There is, however, one point on the screen that is even easier to hit: the point below the cursor. You don't have to move the mouse at all to hit it. Context menus make use of this.

If a menu pops up below the mouse cursor, it makes sense to arrange the individual menu entries around the mouse cursor to decrease the average distance to each entry. One way to achieve this is by using a radial context menu.

Many games use radial context menus. Here's an example from the LucasArts title Full Throttle:

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_140_0.png)

The Firefox extension easyGestures also uses a radial context menu:

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_140_1.png)

So if they work so well, why aren't radial context menus used more often? One reason may be that it's hard to fit a lot of menu entries into a small circle. Maya gets around this by using regular menu labels but arranging them in a circle around the mouse:

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_140_2.png)

A solution retaining the familiar look of traditional context menus yet still offering some of the advantages of radial context menus would be a regular context menu with more than one horizontal level. We could just break up traditional context menus into several smaller groups of commands and then use the horizontal space to arrange them around the cursor.²

2. This is the type of context menu I use in Appway, a business process management system. You can find it at http://www.appway.com.

## Perceiving Circles and Lines

One of the reasons why radial context menus may not be more popular can be found in Vision Science (Pal99) by Stephen E. Palmer. When explaining one model of how humans perceive visual information, he notes that “cells in the first area of the visual cortex have elongated receptive fields that respond most vigorously if stimulated by an edge or line at a particular orientation and position.” In other words, it seems that humans have special mechanisms for seeing lines. What’s more, we may be better at seeing horizontal and vertical lines than lines going in other directions. In Sensation and Perception (Cor99), Stanley Coren speculates that since humans spend most of their time in rectilinear environments and are constantly exposed to vertical and horizontal lines, our brains are biased toward lines in those orientations.

Indeed, a paper called “Perception of contour orientation in the central fovea part I: Short lines” by D.P. Andrews notes that in many experiments, “acuity for orientation was best near the horizontal and vertical directions.” Other research agrees. For example, in a paper titled “Human orientation discrimination tested with long stimuli,” Guy A. Orban comes to the conclusion that “orientation sensitivity is better for a narrow range of orientations around the principal meridians.”

To make a really long story short, research seems to suggest that people perceive horizontal and vertical lines more quickly and correctly than oblique lines or circles.

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_141_0.png)

THE USER HAS TO MOUSE FURTHER TO HIT TARGETS...

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_141_1.png)

...AND LESS FAR WITH THIS MENU

Another benefit of this kind of menu is that better usage of horizontal space allows you to show more menu items at the same time. As a result, you don’t have to hide any menu items inside hard-to-use submenus.
