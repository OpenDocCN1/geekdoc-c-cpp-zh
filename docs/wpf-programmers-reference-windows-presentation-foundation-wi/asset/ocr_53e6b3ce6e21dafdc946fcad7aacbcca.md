# User Interaction Controls

The two preceding chapters described two categories of WPF controls: content controls and layout controls. This chapter describes a third category: user interaction controls.

User interaction controls are the objects that the user manipulates to interact with the application. Where content controls let the program give information to the user, user interaction controls let the user give information to the program.

The types of information the user gives to the program are:

+   - Textual values entered in textboxes
- Choices from list boxes, combo boxes, radio buttons, checkboxes, and so forth
- Values picked from a value selection control such as a slider or numeric up/down button

The user also tells the program when to perform actions by clicking buttons and selecting menu items.

This chapter describes these controls and gives examples to help you get started using them. Because the whole point of these controls is to give information and instructions to the program, this chapter contains a bit more code-behind than the previous ones.

Chapter 2 includes several sections that explain different ways of building event handlers. See the section “Code-Behind” for details.

# CONTROL OVERVIEW

The following table briefly lists the controls described in this chapter together with their purposes. You can use this table to help decide which control you need for a particular purpose.

| CONTROL | PURPOSE |
|---||
| Button | Lets the user click to tell the program to do something. |
| CheckBox | Lets the user select or deselect a non-exclusive option. |