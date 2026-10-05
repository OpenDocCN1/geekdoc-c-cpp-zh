This shows that the virtual starting page is currently mapped to physical address 0x310000.0x21d21000. TestLimit’s -d option writes the program's name to the first bytes of each address. We can demonstrate this with the !dc (display characters using physical address) command in the local debugger:

```
!dc 0x21dc1000
#212d1000 74736554 696d94c 00000074 00000000 TestLimit.....
#212d1010 00000000 00000000 00000000
```

If you’re not quick enough, this—the page may be removed from the working set. For the final leg of the experiment, we will demonstrate that this data remains intact (for a while, anyway) after the process working set is reset and this page is moved to the modified and standby page.

VMMap, having selected the Testlimit, open the Menu and show Empty Working Set to reduce the process’s working set to the bare minimum.
VMap’s display should now look like this:

![](bbox=[0.166, 0.642, 0.638, 0.915])