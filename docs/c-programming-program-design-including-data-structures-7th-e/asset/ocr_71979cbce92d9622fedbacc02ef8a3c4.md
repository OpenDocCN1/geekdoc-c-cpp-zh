Suppose that 10 is to be inserted. After inserting 10 in the list, the node with info 10 becomes the first node of list. This requires us to change the value of first. Also, count is incremented by 1. Figure 16-32 shows the resulting list.

![](bbox=[0.2, 0.21, 0.9, 0.34])

FIGURE 16-32 list after inserting 10

**Case 3:** The list is not empty, and the item to be inserted is larger than the first item in the list. As indicated previously, this case has two scenarios.

**Case 3a:** The item to be inserted is larger than the largest item in the list; that is, it goes at the end of the list. Consider the list shown in Figure 16-33.

![](bbox=[0.2, 0.55, 0.9, 0.68])

FIGURE 16-33 list before inserting 65

Suppose that we want to insert 65 in the list. After inserting 65, the resulting list is as shown in Figure 16-34.

![](bbox=[0.2, 0.78, 0.9, 0.91])

FIGURE 16-34 list after inserting 65