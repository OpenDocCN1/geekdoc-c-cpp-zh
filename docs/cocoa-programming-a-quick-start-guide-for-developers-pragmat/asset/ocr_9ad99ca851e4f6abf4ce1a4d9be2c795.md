![](bbox=[0.136, 0.071, 0.776, 0.58])

The report tells us that an object has been allocated and stored into host with a retain count of 1. You may see three problems reported instead of the one pictured previously—if you click each, you'll see that they are reporting the same issue, and when we fix it, they will all disappear. After host is used in the log statement, it is never referenced again. That's our memory leak. The Greeter object is instantiated and used and then hangs around for as long as the GUI window remains open without ever being used again.

# 6.3 Fixing the Memory Leak on Mac OS X

To fix the memory leak on Mac OS X, go back to your project settings, and change the setting for Objective-C Garbage Collection from Unsupported to Required.