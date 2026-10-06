# Working with a Form's Layout

When you place Controls on a Form in the IDE, you can drag them to any location to achieve the effect you want.

When you drag multiple Controls onto a Form, snap lines appear and help you align new Controls with others in place. Figure 12-29 shows snap lines that you can use to align a second label below the first one. Snap lines also appear when you place a control closer to the edge of a container than is recommended.

You can also use the Location property in Control's Properties list to specify a location. With either technique, code like the following is generated: this.label1.Location = new System.Drawing.Point(23, 19);

![](bbox=[0.104, 0.14, 0.4, 0.396])

Other properties can help you to manage the appearance of a Form (or ContainerControl). For example, setting the Anchor property causes a Control to remain at a fixed distance from the side of a container when the user resizes it. Figure 12-30 shows the properties when a Label that has been placed on a Form. The Anchor property has a drop-down window that lets you select or deselect the sides to which the label should be anchored. For Controls, the default setting for Anchor is Top, Left.

![](bbox=[0.104, 0.453, 0.48, 0.705])

Figure 12-31 shows a Form with two Labels. On the Form, label1 has been anchored to the top left, and label2 shows the Form as it first appears to the user, and the right side shows the Form after the user has resized it. Notice that in the resized Form, label1 is still the same distance from the top as it was originally, and label2 is still the same distance from the bottom right as it was originally. Anchoring is useful when users expect a specific control to always be in the same general location in a container.