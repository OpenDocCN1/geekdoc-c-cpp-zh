coordinates of the point in standard parentheses notation. Now let's use this simple setup to replicate a very common occurrence in software systems, which is that a library we are using is updated to a newer version, but deployed to systems that still have the original version of the calling application in use. In this demo, deployment just means copying a version of the point library into the folder where the main application executable resides. We'll replicate that scenario by changing our point into a point by adding a new field that will hold the Z coordinate for the point. We're going to rebuild just the library, and then "deploy" the updated library to the location where our app is installed. If we rerun our application, which we have not changed or recompiled to be aware of the new field, the application still runs as expected, albeit with a Z field of 0. This demonstrates C# code's resilience to change. When the application developer is ready to opt in to taking advantage of the new functionality available in the library they are using, they can of course rebuild and redeploy their application and now have access to the extended functionality.

```
```text
C:\demo>app
(30, 12)

C:\demo>copy .\deployedLibraries\point3d\point.dll .
Overwrite .\point.dll? (Yes/No/All) y
        1 file(s) copied.

C:\demo>app
(30, 12, 0)

C:\demo>app
(30, 12, 42)

C:\demo>
```
```

This ability to maintain resilience in the presence of changes to dependencies is a hallmark of C# and other managed languages. And to revisit the previous point about safety, should a library developer make some sort of breaking change to a type definition, which I'll