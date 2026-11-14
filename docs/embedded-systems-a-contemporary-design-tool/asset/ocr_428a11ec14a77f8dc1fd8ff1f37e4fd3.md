The proper design executes a break-before-make switch by using two control lines. Before turning the bus around, the first step is to direct all devices to release the bus. This is accomplished by placing the enable control line into the logical 0 state. Then the state of the direction control is changed. Finally, the devices are re-enabled onto the bus by placing the enable control line into the logical 1 state. The design appears in Figure 16.14.

![](bbox=[0.26, 0.18, 0.78, 0.51])

# Figure 16.14 A Bidirectional I/O Bus – design 2

From the preceding timing diagrams, it is evident that the CPU must be involved in each aspect at the exchange. Furthermore, the transfer rate for any such exchange is determined by the rate at which the device can read or write data. A slower device can place a significant burden on the CPU operation. It should be evident that utilizing the CPU in such an activity in higher performance systems is not the best use of the resource.

On the software side of the picture, we have the following code fragments in Figure 16.15. In each case, anAddress is the address of the target device in I/O address space.

```
```c
"anAddress = aValue; // Write to anAddress
aValue = "anAddress; // Read from anAddress

Assembler
LD aReg, anAddress; // Register <- anAddress
ST anAddress, aReg; // anAddress <- Register
```
```

# Figure 16.15 C and Assembler Code Fragments For a Write and Read Operation to and From an I/O Device