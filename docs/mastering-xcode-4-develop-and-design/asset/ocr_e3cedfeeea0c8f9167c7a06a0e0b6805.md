![](bbox=[0.282, 0.171, 0.865, 0.356])

![](bbox=[0.282, 0.392, 0.864, 0.576])

The debugger will respond by logging the string returned when the NSURL object is asked for its -description. **Figure 17.22** shows the results in the debugger console. You can also print self when stopped within a method belonging to an instance of an Objective-C class. In the current scope of the example, self refers to an instance of the TestAppAppDelegate class. **Figure 17.23** shows the result of printing self in this scope. In this case, the TestAppAppDelegate class doesn’t override -description, so the information displayed is the default description format inherited from NSObject. That is, the class name and address of the instance being printed are given.

Of course you can also print objects through the accessors of other objects. For example, NSURL has a string property called -scheme. To print the scheme of the NSURL instance assigned to googleURL, you can issue the following command:

```
```text
po [googleURL scheme]
```
```