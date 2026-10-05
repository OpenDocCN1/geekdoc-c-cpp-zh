Free: 3076 ( 12304 kb)
Standby: 4669104 (1867416 kb)
Modified: 7845 ( 31380 kb)
ModifiedNoWrite: 117 ( 468 kb)
Active/Valid: 3677990 (14711960 kb)
Transition: 5 ( 20 kb)
Bad: 0 ( 0 kb)
Unknown: 1277 ( 5108 kb)
TOTAL: 8346281 (33457124 kb)

Using the kernel debugger imemage command, you can obtain similar information, although through this will take considerably longer to execute.

# Page list dynamics

Figure 5-37 shows a state diagram for page frame transitions. For simplicity, the modified-no-free, bad and ROM lists aren't shown.

![](bbox=[0.125, 0.405, 0.685, 0.725])

FIGURE 5-37 State diagram for physical pages.

Page frames move between the paging lists in the following ways:

+   - When the memory manager needs a zero-initialized page to service a demand-zero page fault (reference to a page that is defined to be all zeroes or a user-mode committed private page that has never been accessed), it first attempts to get from the zero page list. If the list is empty, it gets one from the free page list and zeroes the page. If the free list is empty, it goes to the standby list and zeroes that page.