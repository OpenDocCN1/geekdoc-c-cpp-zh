
# Listing 7-3. The Implementation of an Instance Method

```objc
1 - (id)initWithName:(NSString*)newName atFrequency:(double)newFrequency {
2 self = [super init];
3 if (self != nil) {
4 _name = newName;
5 _frequency = newFrequency;
6 }
7 return self;}
```

Listing 7–3 illustrates the implementation of one of the instance methods of your radio station class. An initialization method accepts a new name and frequency. Many OS X and iOS classes have similar initialization instance methods. Instead of initializing the class and then individually setting various values, many class initialization methods allow special initialization methods, or, in this case, multiple values to be passed on initialization.

In the preceding example, line 1 is the interface of your method, and it contains two parameters: newName and newFrequency. To use this method, the caller would simply do the following:

```objc
RadioStation my = [[RadioStation alloc] initWithName:@"WOW FM" atFrequency:102.5];
```

This method is also defined to return an id. An id is a generic object, and all Objective-C objects are of the type ‘id’, just like the RadioStation is an object. Now, let's look at the rest of the implementation.

Line 2 references special variables that you don't have to define anywhere. The keyword self is used to mean “this instance of class,” so line 2 is assigning “this instance of class”—the value returned from the use of the special variable: super init. The keyword self is short for “superclass,” which can be thought of “parent of the class.” Any initialization method will typically be thought of as something that looks similar to line 2.

Why is line 2 even necessary? Well, if you have an object that is derived from another object (remember, the class is RadioStation : NSObject), you must tell the parent object to initialize itself. The parent does the same by telling its parent to initialize itself, and so on, until the topmost object is reached. If another class uses yours as a parent, your code would also have to get an init call so RadioStation could be initialized. This is standard issue in the real world of Objective-C. A class needs to tell its parent to initialize when the class is created, and it needs to tell its parent to de-allocate itself whenever the class is going away.

Line 3 checks to whether the [super init] call worked. If it worked, the value of self would be something other than nil, a value that effectively means “not initialized.”

Lines 4 and 5 set up the instance variables of this class to the values passed into this method.

Line 8 returns self to the caller. Just like the call to [super init], your initialization function needs to return the new object back to the caller.

# Using Your New Class

You've created a simple RadioStation class, but by itself, it doesn't accomplish a whole lot. In this section, you will create the Class and maintain a list of RadioStation classes.

# Creating Your Project

Let's start up Xcode (see Figure 7–1) and create a new project named RadioStations.

![](img/322e107ddf8f5cd963a6efafdcd86f38_146_0.png)

Figure 7–1. Open Xcode so you can create a new project.

- 1. Make sure you choose an iOS application and select the Single Application template, as shown in Figure 7–2.
- 2. Once you've selected the template, click the Next button.

![](img/322e107ddf8f5cd963a6efafdcd86f38_147_0.png)

**Figure 7–2. Selecting a template in the new project window**

- 3. Next, set the Product Name (Application name) to RadioStations.
- 4. Set the Company Identifier (a pretend company will do) and set the Device Family to iPhone (as shown in Figure 7–3). Also, make sure that “Use Automatic Reference Counting” is checked.

# CHAPTER 7: Objective-C Classes, Objects, and Methods

![](img/322e107ddf8f5cd963a6efafdcd86f38_148_0.png)

Figure 7-3. Naming the new iPhone application

- 5. Click the Next button and Xcode will ask you where you want to save your new project. You can save the project on your Desktop or anywhere in your Home folder. I like the Desktop because it's easy to spot. Once you've made your choice, simply click the Create button.
- 6. Once the Create button has been clicked, the Xcode Workspace Window should be visible, as shown in Figure 7–4.

# CHAPTER 7: Objective-C Classes, Objects, and Methods

![](img/322e107ddf8f5cd963a6efafdcd86f38_149_0.png)

# Adding Objects

Now, you can add your new objects.

- 1. First, create your RadioStation object. Right-click the RadioStations group folder and select New File... (as shown in Figure 7–5).

![](img/322e107ddf8f5cd963a6efafdcd86f38_149_1.png)

- 2. The next screen, shown in Figure 7–6, asks for the new file type. Simply choose Objective-C class from the Cocoa Touch group, and then click Next.

![](img/322e107ddf8f5cd963a6efafdcd86f38_150_0.png)

**Figure 7–6.** Selecting the new file type

- 3. On the next screen, enter “RadioStation” as the class and select NSObject as the “Subclass Of.” This means that your new class will be a subclass of NSObject, as shown in Figure 7–7.

# CHAPTER 7: Objective-C Classes, Objects, and Methods

![](img/322e107ddf8f5cd963a6efafdcd86f38_151_0.png)

Figure 7–7. Choosing your new object's subclass

- 4. The next screen asks you where to create the files. Simply click the Create button, since the location in Xcode chooses to save the files is within the current project, as shown in Figure 7–8.

![](img/322e107ddf8f5cd963a6efafdcd86f38_152_0.png)

Figure 7–8. Choosing where to create files

- 5. Your project window should now look like Figure 7–9.

![](img/322e107ddf8f5cd963a6efafdcd86f38_152_1.png)

Figure 7–9. Your project window

# Writing the Implementation

The RadioStation.h now defines the instance variables, class methods, and instance methods. Let's move on to the implementation file.

- 1. The implementation file you use here has been simplified from our example, but will work perfectly for our station simulation.
- 2. Your project window should now look like Figure 7–10.

![](img/322e107ddf8f5cd963a6efafdcd86f38_153_0.png)

Figure 7–10. Implementation

- (id)initWithName:(NSString*)newName atFrequency:(double)newFrequency {
    self = [super init];
    if (self != nil) {
        _name = newName;
        _frequency = newFrequency;
    }
    return self;
}
- (NSString *)name {
    return _name;
}
- (void)setName:(NSString *)newName {
    _name = newName;
}
- (double)frequency {
    return _frequency;
}
- (void)setFrequency:(double)newFrequency {
    _frequency = newFrequency;
}

# Listing 7–4. TheStation Implementation File

```objc
#import "RadioStation.h"

@implementation RadioStation

- (id)initWithName:(NSString*)newName atFrequency:(double)newFrequency {
    self = [super init];
    if (self != nil) {
        _name = newName;
        _frequency = newFrequency;
    }
    return self;
}

- (NSString *)name {
    return _name;
}

- (void)setName:(NSString *)newName {
    _name = newName;
}

- (double)frequency {
    return _frequency;
}

- (void)setFrequency:(double)newFrequency {
    _frequency = newFrequency;
}

@end
```

# Listing 7–5. The Updated ViewController.h Interface File

```objc
#import <UIKit/UIKit.h>

@class RadioStation;

@interface ViewController : UIViewController {
    RadioStation *myStation;
    IBOutlet UILabel* stationName;
    IBOutlet UILabel* stationFrequency;
    IBOutlet UILabel* stationBand;
}
@end
```

# Listing 7–6. The ViewController.m file

```objc
#import "ViewController.h"

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    // Initialization code will go here
}

@end
```
