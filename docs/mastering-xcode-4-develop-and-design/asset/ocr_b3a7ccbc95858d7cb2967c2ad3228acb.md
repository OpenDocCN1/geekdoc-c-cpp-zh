![](bbox=[0.135, 0.171, 0.718, 0.242])

**Figure 20.26** shows the complete lifecycle of the memory address in question. The telltale entry is the one that shows a −1 under the RefCt (reference count) column. A message was passed to that zombie. Double-click each entry to see the code (really any entry will do since the entire history happened within three consecutive lines of code).

The history shown in Figure 20.26, along with enabling us to navigate to the point in the code where the object was messaged when it should have died, is invaluable for discovering the flaw in logic that led to the memory management bug. Because it is displaying the history of a *memory address* rather than the history of the object itself, it’s important to keep in mind that you may see entries from the lifecycles of *other* objects that lived at that address as well. Look for the telltale −1 reference count to make sure you’ve got the right object.

> **TIP:** You might have noticed that the Zombies template is actually just the same old Allocations instrument. The difference is in the extra options switched on in its info popover (click the *i* button to the right of the instrument in the Instruments list).

# MANY OTHER INSTRUMENTS

There are a number of other excellent Instruments templates and nowhere near enough space in this book to detail them. There are templates for analyzing memory management, garbage collection, multicore processes, Grand Central Dispatch queues, file system access, and Lion’s Autolayout, and there’s even a UI recorder that can record and play back user interface events for repeated UI testing. See the Instruments documentation via its Help menu for more details.