# Building Three Sample Apps

You can build services in C# in a few ways, as described in the next three chapters. This section’s heading isn’t exactly right, however. I show you how to build the same app in three different ways. The app, the SHARP conference management system (or a simple version of it), was built using these formats:

+   - **ASMX:** This first version is in the venerable ASMX format: ASP.NET Web services. Though this format has been largely superseded by WCF, it’s still available. I cover it in this chapter and the next because it’s a viable solution for certain situations.
+   - **WCF:** Windows Communication Foundation (WCF), the most important service platform, is given enough screen time here to get you started. The topic is broad, and you can find lots of references to other resources.
+   - **REST:** REpresentational State Transfer (REST), the oldest service protocol on the planet, has a new life, thanks to AJAX. REST isn’t a first-class citizen in the .NET world, but it’s important.

The entire process uses a single entity data model, shown in Figure 1-6, and provides allowed operations to it.

![](bbox=[0.15, 0.5, 0.8, 0.85])

Figure 1-6:
The simplified SHARP data model.