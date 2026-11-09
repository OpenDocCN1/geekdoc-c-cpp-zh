
```objc
-(void)awakeFromNib{
    [self addObserver:self
           forKeyPath:@"totalCount"
              options:NSKeyValueObservingOptionNew
              context:NULL];
}
-(void)observeValueForKeyPath:(NSString *)keyPath
                     ofObject:(id)object
                       change:(NSDictionary *)change
                      context:(void *)context {
    NSLog(@"%@", self.totalCount);
}
@end
```

In addition to keyPathsForValuesAffectingTotalCount, we register the observer in the awakeFromNib method. We also have a getter method for totalCount that returns the sum of countOne and countTwo. This is called from the observeValueForKeyPath:ofObject:change:context: method whenever either value is changed. In response, we just log the total to the Console.¹

This chapter took you through the fundamentals of observing.² You register an object and wait until it is called back. This is like a notification without a notification center. This is just a relationship between two objects, and only the observer needs to know about the observed. You've seen how to register multiple observers to one attribute and how to register a single observer to multiple attributes. Finally, you saw how to set up a dependent variable so its observers were updated when the variables it depends on change.

As cool as KVO and KVC are both individually and together, their real power is in the technologies they enable. We'll strip out code from the controller layer with Bindings and from the model layer with Core Data.

You can use KVO and KVC whether you're developing for Mac OS X or for iPhone OS. If you are mainly interested in developing for Mac OS X, you're going to love where we're headed next. We're going to see how these technologies enable bindings, which let you write less code for the controller layer. Unfortunately, there currently isn't any support for bindings for iPhone OS.

- 1. See KVO/Counter1 in the code zip file to see that you can remove the totalCount instance variable and property and still get this same behavior.
- 2. You can find more information in Apple's Key-Value Observing Guide [App08].

## Chapter 21: Cocoa Bindings

So far, we’ve used Interface Builder to create our GUI and to connect buttons, labels, tables, and more to controllers and models. This eliminates a lot of boilerplate code. You don’t need to inherit from an NSButton and configure its look and placement in code. You know from your work with custom views that you can write that code—you just don’t have to do this.

Cocoa Bindings looks at the controller layer and asks how much of the repetitive code can be removed. It turns out, if you are careful to work with KVO- and KVC-compliant classes, the answer is “most of it.” Much of this chapter will find us back in Interface Builder making connections and typing in keypaths. We’ll have a little bit of code to write but not much.

We’ll start this chapter by creating a new Cocoa application named CounterWithBindings. You will add a new Objective-C class named Counter, declare a property named count of type NSNumber, and synthesize it. That’s all the code you’re going to need to write to create your model.

As for the view, you’ll drag a stepper and a text field into the window. We’ll add more as the chapter progresses, but that will be good enough to begin with.

That leaves us with the controller. In this chapter, you won’t be implementing the controller in code. You’ll use Cocoa Bindings and the fact that your model is KVC and KVO compliant to create your controller using Interface Builder. Cocoa Bindings will let the view and model communicate without us writing a lot of boilerplate glue code. We’ll start by revisiting our example from the previous chapter.

### 21.1 The Model and View for Our Counter with Bindings

Create a new project named CounterWithBindings. Add a new Objective-C class named Counter that contains the property count. In other words, you add two lines of code to the header file template:

```
Download Bindings/CounterWithBindings/Counter.h

#import <Cocoa/Cocoa.h>

@interface Counter : NSObject {
    NSNumber *count;
}
@property(copy) NSNumber *count;

@end
```

You also need to add one line of code to the implementation to synthesize the property count:

```
Download Bindings/CounterWithBindings/Counter.m

#import "Counter.h"

@implementation Counter

@synthesize count;

@end
```

We have a single class with a single property defined. There will be no other code in this application for the first part of this chapter.

Now let’s create the view. Drag a stepper and a text field into the main window. As before, use the Attributes inspector so that the stepper’s behavior is set to Value Wraps. Resize the window to look like this:

![](img/9355405953264484a02198b0e3d25b7e_334_0.png)

OK. Now we have our model and our view. Let’s create the controller.

### 21.2 Creating and Connecting the NSObjectController

In Interface Builder, drag a Counter object from the Library, and drop it on the Document window. This is the instance of your model.

**Joe Asks…**

**Wouldn’t Code Be Better?**

Depending on your background, it sure can feel like that. A lot of the logic now moves to files you set up with Interface Builder. When you have a problem, you can’t use the techniques you’ve been using forever. Initially, it is harder to locate problems. On the other hand, you’re less likely to create these problems by making mistakes in what should be boilerplate code.

Cocoa Bindings can be scary. But soon you’ll get a feel for where you should look when things go wrong. If you think back to your early days coding, the same thing was true there. You had to learn where to look for problems. You probably stared long and hard before you found that you typed = when you meant to type ==. So, this isn’t a new frustration so much as a new frontier for an old one.

Next, drag an NSObjectController from your Library to the Document window. Remember back to our early examples in this book. The controller sits between the model and the view. The controller insists on being an intermediary. You will need to configure your controller by following these three steps:

- 1. Connect to the object that the object controller is controlling.
- 2. Specify which keys the object controller is responsible for.
- 3. Bind each element to a property that the object controller is controlling.

**Connecting the Controller**

The object controller needs to know which object it is controlling. Click the object controller, and look in the Connections inspector for its content outlet. Connect this content connection to the Counter object. You can (and soon will) have more than one object of the same type. This is the step where you are specifying which one the object controller is responsible for.

**Selecting the Keys**

Next you'll need to make the count key available to objects that bind to the NSObjectController. Select the object controller, and use the Attributes inspector to set the class name to Counter. Notice that there are two modes. We are using the class mode here because Counter is a class. When we build data models with Core Data, we will use the entity mode.

You have to explicitly specify which keys the object controller will make available for binding. Here there is only one possible choice. Use the plus sign to add the key count.

![](img/9355405953264484a02198b0e3d25b7e_336_0.png)

**Binding a Component**

Click the text field to select it, and open its Bindings inspector using ⌘ 4 or just by clicking the inspector's fourth tab.

![](img/9355405953264484a02198b0e3d25b7e_337_0.png)

In the Value section, select the “Bind to” checkbox, and use the drop-down list to select Object Controller. The controller key is selection, and the model key path is count. Do the same for the stepper.

Both the stepper and the text field are bound to the value of count. Click Build & Run. Click the stepper, and you can see the values of the text field are changed. So far, this doesn’t seem like a very big win. But it is.

When you click the stepper, its value is bound to the value of count, so count is updated automatically. Similarly, the text field is bound to the value of count. Whenever the value of count changes, the text field is automatically updated. The connections are made through the controller. There is a lot of activity going on here. In the next section, we’ll add more widgets to make this clearer.

### 21.3 Binding More Objects

Add a circular slider and a horizontal slider to the view. Bind each to the count by using the object controller.
