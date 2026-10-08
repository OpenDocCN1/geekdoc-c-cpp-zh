```
//fill oval in yellow
theColor = [NSColor colorWithDeviceRed:(float)1.0
green:(float)1.0 blue:(float)0.0
alpha:(float)1.0];
[theColor set];
[thePath fill];

//create oval path
theRect = NSMakeRect(100, rect.size.height-80, 60, 60);
thePath = [NSBezierPath bezierPathWithOvalInRect:theRec
t];

//fill oval in red
theColor = [NSColor colorWithDeviceRed:(float)1.0
green:(float)0.0 blue:(float)0.0
alpha:(float)1.0];
[theColor set];
[thePath fill];
```

Figure 12-7 shows the results.

![](bbox=[0.25, 0.48, 0.63, 0.72])

**Figure 12-7:** Add a few round ovals to create an image of a simple traffic light.

# ## Drawing a path

You don't have to fill all paths that you run across. You can also *stroke* a path, which has the effect of drawing an outline around a path. Stroking a path is just as simple as it is to fill one: