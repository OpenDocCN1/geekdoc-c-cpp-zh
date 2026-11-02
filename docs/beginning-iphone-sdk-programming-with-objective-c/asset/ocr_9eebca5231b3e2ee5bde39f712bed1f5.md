![](bbox=[0.06, 0.14, 0.45, 0.55])

FIGURE 11-17

# How It Works

So far, all the work that has been done prepares the UI for displaying the values retrieved from the preferences settings. In particular, you need to prepare the Picker view to display a list of colors from which the user can choose. In the Flipside view, you make use of the Done button to save the values of the preferences settings. That is, your code for saving the preferences settings will be inserted into the done action (this will be done in the “Saving the Settings Values” section).

To load the Picker view with the three colors, you first need to ensure that the FlipsideViewController class conforms to the UIPickerViewDataSource and UIPickerViewDelegate protocols:

```
//---FlipsideViewController.h---
@protocol FlipsideViewControllerDelegate;

@interface FlipsideViewController : UIViewController <UIPickerViewDataSource, UIPickerViewDelegate> {
    id <FlipsideViewControllerDelegate> delegate;
}
```

The UIPickerViewDataSource protocol defines the methods to populate the Picker view with items while the UIPickerViewDelegate protocol defines methods to enable users to select an item from the Picker view.