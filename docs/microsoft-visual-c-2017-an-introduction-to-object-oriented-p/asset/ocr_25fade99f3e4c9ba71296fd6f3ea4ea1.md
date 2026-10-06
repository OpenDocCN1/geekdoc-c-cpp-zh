# CHAPTER 12 Using Controls

If you precede a letter with an ampersand (&) in the Text property value of a ButtonBase object, an access key provides a shortcut way for a user to make a selection using the keyboard. For example, if a Button's text is defined as &Press, then typing Alt + P has the same effect as clicking the Button. Access keys are also called hot keys.

You can place multiple RadioButtons on a Form using a GroupBox or Panel1. You will learn more about GroupBoxes and Panels later in this chapter.

Figure 12-13 shows an example of a Form with which a user can select pizza options. It contains several Labels, four CheckBoxes, and three RadioButton objects. It makes sense for the pizza topping choices to be displayed using CheckBoxes because a user might select multiple toppings. However, options for delivery, pick-up, and dining in the restaurant are mutually exclusive, so they are presented using' objects.

![](bbox=[0.136, 0.396, 0.538, 0.663])

When you add CheckBox and RadioButton objects to a form, they are automatically named using the same conventions you have seen with Buttons and Labels. That is, the first Check assigned name is checkbox1 by default, the second is named checkbox2, and so on. Using the Properties list, you can assign meaningful names such as sausageCheckBox and pepperoni1 Naming objects appropriately makes your code more understandable to others, and makes your programming job easier.

**Figure 12-13** A Form with Labels, CheckBoxes, and RadioButtons

Both CheckBox and RadioButton objects have a Checked property whose value is true or false. For example, if you want to add $1.25 to a pizzaPrice

you create a CheckBox named sausageCheckBox and you want to add when the user checks the box, you can write the following:

```
if(sausageCheckBox.Checked)
   pizzaPrice = pizzaPrice + 1.25;
```