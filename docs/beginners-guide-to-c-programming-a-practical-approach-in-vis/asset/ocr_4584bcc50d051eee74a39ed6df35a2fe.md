```
CallByReference(ref myString);
MessageBox.Show("Value of the string after passed to CallByReference() method: " + myString);
}
}
```

Code 11.22 (cont'd)

We can now build and run the project again. When we click the Show Button, the initial value of myString will be displayed as before:

![](bbox=[0.32, 0.4, 0.68, 0.6])

Figure 11.11. Initial value of myString displayed as before

When we click the OK button in the message box, myString variable will be passed to our CallByReference() method by reference and then its current value will be displayed in the message box:

![](bbox=[0.25, 0.8, 0.75, 0.92])

Figure 11.12. The current value of myString

As it is seen in the message box, the value of the original variable myString is altered when callByReference() method called it by reference. Hence, we see the difference of calling by value and calling by reference clearly in these simple examples.