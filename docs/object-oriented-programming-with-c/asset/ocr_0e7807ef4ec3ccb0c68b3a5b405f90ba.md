```
test T2,T3;
cout<<"\n\nLeaving Block 1.."}
cout<<"\n\nBack inside the main block.."return 0;
}
```

The output of Program 6.7 would be:

+   Inside the main block..
+   Creating first object T1..
+   Constructor Msg: Object number 1 created..
+   Inside Block 1..
+   Creating two more objects T2 and T3..
+   Constructor Msg: Object number 2 created..
+   Constructor Msg: Object number 3 created..
+   Leaving Block 1..
+   Destructor Msg: Object number 3 destroyed.
+   Destructor Msg: Object number 2 destroyed.
+   Back inside the main block..
+   Destructor Msg: Object number 1 destroyed..

> NOTE:A class constructor is called everytime an object is created. Similarly, as the program control leaves the current block the objects in the block start getting destroyed and destructors are called for each one of them. Note that the objects are destroyed in the reverse order of their creation. Finally, when the main block is exited, destructors are called corresponding to the remaining objects present inside main.

Similar functionality as depicted in Program 6.7 can be attained by using static data members with constructors and destructors. We can declare a static integer variable count inside a class to keep a track of the number of its object instantiations. Being static, the