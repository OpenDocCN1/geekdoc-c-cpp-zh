```
//---declaring the outlet---
IBOutlet UITextField *txtName;
}

//---expose the outlet as a property---
@property (nonatomic, retain) UITextView *txtName;

//---declaring the action---
-(IBAction) btnClicked: (id) sender;

@end
```

The IBOutlet identifier is used to prefix variables so that Interface Builder can synchronize the display and connection of outlets with Xcode. The @property keyword indicates to the compiler that you want the txtName outlet to be exposed as a property. The nonatomic keyword indicates that there is no need to ensure that the property is used in a thread-safe manner because it is not used in multiple threads. The default behavior is atomic, and specifying nonatomic actually improves the performance of your application.

> NOTE The IBOutlet tag can also be added to the @property identifier. This syntax is common in the Apple documentation:
> 
> @property (nonatomic, retain) IBOutlet UITextField *txtName;

> NOTE For the use of the nonatomic and retain identifiers, refer to Appendix D, where you can find an introduction to Objective-C, the language used for iPad programming. Also, the @synthesize keyword, discussed shortly, is explained in more detail there as well.

The IBAction identifier is used to synchronize action methods. An action is a method that can handle events raised by views (for example, when a button is clicked) in the View window. An outlet, on the other hand, allows your code to programmatically reference a view on the View window.

Once your actions and outlets are added to the header (.h) file of the View Controller, you then need to connect them to your views in Interface Builder.

When you control-click and drag the File's Owner item to the TextField view and select txtName, you essentially connect the outlet you have created (txtName) with the TextField view on the View window. In general, to connect outlets you control-click and drag the File's Owner item to the view on the View window.

> WARNING A quick tip: to connect outlets to the views, you drag the File's Owner item onto the required view in the View window.