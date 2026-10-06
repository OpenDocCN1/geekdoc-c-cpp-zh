```
- (IBAction) clickl;
@end
```

Notice that iPhone applications import the header file <UIKit/UIKit.h>. This header file, in turn, imports other UIKit header files, in a similar way that the Foundation.h header file imported other header files you needed, such as NSString.h and NSObject.h.

# Note

As noted previously in this text, using an instance variable name that's different from the property name encourages you to access the instance variable through the property and not directly by the variable's name. Apple has been encouraging this style of coding.

You added a property belonging to the UILabel class display. This will be an outlet property that will be connected to a label. When you set this property's text field, it updates the corresponding text for the label in the window. Other methods defined for the UILabel class allow you to set and retrieve other attributes of a label, such as its color, the number of lines, and the size of the font.

You'll want to use other classes in your interface as you learn about iOS programming that we won't describe. The names of some of these you give a clue as to their purpose: UITextField, UIColor, UIView, UITableView, UIImageView, UIImage, UISlider, and UIButton.

The property is an outlet, and in the property declaration, note the use of the IBOutlet identifier. IBOutlet is really