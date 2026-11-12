![](bbox=[0.05, 0.17, 0.7, 0.5])

Then let's say we have a function that consumes vehicles: canVehicleReachLocationInTime(Vehicle* vehicle, Location* location, Time* deadline). We could pass any instance of Boat, Airplane, Car, Maserati, or Yugo to this function. Similarly, we could pass any Car, Maserati, or Yugo object to the estimatedTimeToFinishIndy500(Car* sampleCar) function.

We will frequently run into inheritance and class hierarchies when we interact with Cocoa Touch view objects (**Figure 2.1**). UIView inherits from UIResponder, which inherits from NSObject. NSObject is a root class—almost all other objects inherit from it. There are a few exceptions (e.g., NSProxy) but these are unusual corner cases.

The NSObject root class ensures that all objects have a basic set of methods (memory management, testing for equality, testing for class membership, and the like). Next, UIResponder adds an interface for objects that respond to motion and touch events, allowing them to participate in the responder chain. Finally, UIView adds support for managing and displaying rectangular regions on the screen.

Figure 2.1 also shows a few subclasses of UIView. As you can see, some screen elements (like UILabel) inherit directly from UIView. Others (UIButton and UITextField) inherit from UIControl, which adds support for registering targets for events, and for dispatching action messages when the events occur.