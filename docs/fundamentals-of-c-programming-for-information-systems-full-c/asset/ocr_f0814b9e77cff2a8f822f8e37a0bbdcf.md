# Arguments and Parameters

The data items that are passed to a method by the calling program are called **arguments**. Thus, the values 72 and 22 in the call statement ComputeTrainingRate(72, 22) are arguments.

The variables declared in the header of a method to receive the arguments are called **parameters**. (As you will see later, parameters also may be used to pass values from the method to arguments in the calling program.) Thus, restingRate and age declared in the header of the method

```
private void ComputeTrainingRate(float restingRate, float age)
```

are parameters.

The arguments are passed to the parameters in the order in which they appear in the argument list. That is, the first argument is passed to the first parameter, the second argument to the second parameter and so on. When ComputeTrainingRate is called, the following assignments take place automatically:

```
ComputeTrainingRate(72, 22);
```

![](bbox=[0.3, 0.47, 0.7, 0.55])

```
private void ComputeTrainingRate(float restingRate, float age)
```

That is,

```
restingRate = 72;
age = 22;
```

The position of an argument in the argument list may be different from that of the corresponding parameter, if the name of the parameter is specified, as in

```
ComputeTrainingRate(age: 22, restingRate: 72);
```

The data type of the parameters and those of the arguments must be compatible—that is, they must obey the rules for assigning values to variables (discussed in Chaper 2).

Let’s see how it works:

**Step 1-11:** Insert a break inside ComputeTrainingRate at the left brace (line 40) by clicking on the left margin.

Insert a second break inside the Click event handler at the call statement (line 54).

Run the form. Note that the TextBoxes and the ListBox on the form are not used in this version of the form.

Click the button to compute the training rate. The program breaks at the call statement. Click Continue. The program breaks at the left brace inside the method.

Move the pointer over the parameters restingRate and age to observe their values, 72 and 22, respectively.

Click Continue to display the training rate.

**Step 1-12:** Repeat Step 1-11 after changing the resting rate and age in the call statement.