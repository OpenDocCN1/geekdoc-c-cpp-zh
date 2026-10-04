# 700 Constructing User Controls

That phone number control consists of things that you already have around you: text box controls, client-side scripting, and validation. All that you need is to put them together.

The technology that you use to combine controls in useful ways is called a User Control, or ASCX. ASCX is encapsulated, easy to create, and easier to use. (ASCX is the file extension for the markup files for these controls.)

# Making a new phone number user control

To show what I mean, here's how to make my favorite user control: the Phone Number control. In this incarnation, it is only good for U.S. format, but that's okay. It gets the point across. Just follow these steps to create a phone number control:

+   1. In the project you've been using in this chapter, right-click the project file and choose Add->New Item.
2. Select Web User Control (see Figure 3-9).
I named it PhoneNumber.ascx.

![](bbox=[0.218, 0.506, 0.858, 0.863])

Figure 3-9: Adding the Phone Number control.
There are no controls in this group. Drag an item from the toolbox to add it to the nodes.