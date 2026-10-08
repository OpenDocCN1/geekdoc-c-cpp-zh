+   4. Connect the **NSMatrix** to an outlet of a **Controller** class by **Control+dragging** from the controller to the NSMatrix control.

When connecting an outlet to an NSMatrix, make sure that you Control+drag from the Controller class to the entire matrix, not to an element of the matrix. If one element becomes highlighted when you Control+drag from the controller to the NSMatrix, move the cursor around until a dark outline appears around the entire NSMatrix (see Figure 9-11).

![](bbox=[0.06, 0.16, 0.2, 0.24])

![](bbox=[0.06, 0.25, 0.8, 0.55])

After you have an outlet to the NSMatrix, you can find out which element the user selected in code by using the selectedRow method of NSMatrix. The selectedRow method returns an integer indicating the index of the currently selected row. Row numbers start from the top, with the first row having an index of 0. To illustrate, here’s a sample action that checks the selectedRow of colorRadios. Based on the index, it displays a message in the console telling you which color was chosen:

```
```
- (IBAction) doSomething: (id) sender
{
    switch ( [colorRadios selectedRow] )
    {
        case 0:
            NSLog(@"User chose red.");
            break;
        case 1:
            NSLog(@"User chose green.");
            break;
        case 2:
            NSLog(@"User chose blue.");
            break;
    };
}
```
```