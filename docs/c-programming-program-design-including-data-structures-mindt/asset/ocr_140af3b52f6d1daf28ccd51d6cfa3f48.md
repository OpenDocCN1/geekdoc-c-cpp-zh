change the values of **first** and **last**. The link field of the previous node—that is, **17**—changes. After deletion, the node with **info 17** contains the address of the node with **24**.)

![](bbox=[0.183, 0.158, 0.91, 0.287])

FIGURE 16-26  *List after deleting 37*

**Case 3b:** The node to be deleted is the last node. Consider the list shown in Figure 16-27. Suppose that the node to be deleted is **54**.

![](bbox=[0.183, 0.403, 0.91, 0.528])

FIGURE 16-27  *List before deleting 54*

After deleting **54**, the node with **info 24** becomes the last node. Therefore, the deletion of **54** requires us to change the value of the pointer **last**. After deleting **54**, **last** contains the address of the node with **info 24**. Also, **count** is decremented by 1. Figure 16-28 shows the resulting list.

![](bbox=[0.183, 0.687, 0.91, 0.816])

FIGURE 16-28  *List after deleting 54*

**Case 4:** The node to be deleted is not in the list. In this case, the list requires no adjustment. We simply output an error message, indicating that the item to be deleted is not in the list.