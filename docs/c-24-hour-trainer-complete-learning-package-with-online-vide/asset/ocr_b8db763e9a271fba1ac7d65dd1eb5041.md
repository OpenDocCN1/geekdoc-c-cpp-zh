property to Public, either in the Form Designer or in code. Now other forms can see the control and change its properties.

> NOTE Controls on a form are private to prevent other pieces of code from accidentally messing them up. By making a variable public, you remove this safeguard. In technical terms, you have weakened the form’s encapsulation—its ability to hide its internal details from the outside world.
> 
> In this case, you want to allow access to this label’s Text property so marking the label as public is reasonable. However, by making the label public you make all of its properties, methods, and events public, not just its Text property.
> 
> A more restrictive approach would be to add a public SetCaption method to the ColorForm. Then other code would call that method instead of setting the label’s text directly. You learn how to build those kinds of methods in Lesson 20.

# TRY IT

In this Try It, you create an application similar to the one shown in Figure 9-5. When the user clicks the main form’s buttons, the program displays the other forms non-modally.

![](bbox=[0.1, 0.65, 0.85, 0.88])

FIGURE 9-5