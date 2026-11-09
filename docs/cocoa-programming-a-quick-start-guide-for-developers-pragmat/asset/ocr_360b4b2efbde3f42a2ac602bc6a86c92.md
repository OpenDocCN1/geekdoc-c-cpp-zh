Click Build & Run, and the application behaves correctly. It creates the new object, displays it properly, and then releases it and calls dealloc.

```
```text
Greeter name: Maggie
created 2009-09-17 14:12:09 -0400
In Greeter dealloc:
```
```

If instead you click Build & Analyze, you’ll see that two problems are flagged in FlashlightAppDelegate.m. You’ll usually see this problem when the method that returns an object (in our case greeterFor:) is defined in a different class than the object that calls it. For this example, both halves of the transaction are included in the same object, and that’s why we successfully created and released the object when we ran the example. The Clang Static Analyzer, however, is identifying a potential problem by looking at the two methods, greeterFor:() and applicationDidFinishLaunching:(), separately.

![](bbox=[0.136, 0.381, 0.776, 0.818])

The second error is telling us that we released an object we didn’t own. In fact, if you look at the applicationDidFinishLaunching: method, you’ll see that when we released host we had no way of knowing that we owned it.