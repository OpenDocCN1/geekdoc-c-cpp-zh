Because first is NULL, we execute statements 5a and 5b. Figure 17-14 shows the resulting list.

![](bbox=[0.204, 0.165, 0.889, 0.269])

**FIGURE 17-14** List after inserting `newNode` in it

We now repeat statements 1 through 6b. After statement 1 executes, num is 15. Statement 2 creates a node and stores the address of this node in newNode. Statement 3 stores 15 in the info field of newNode, and statement 4 stores NULL in the link field of newNode (see Figure 17-15).

![](bbox=[0.204, 0.417, 0.889, 0.534])

**FIGURE 17-15** List and `newNode` with `info` 15

Because first is not NULL, we execute statements 6a and 6b. Figure 17-16 shows the resulting list.

![](bbox=[0.204, 0.649, 0.889, 0.759])

**FIGURE 17-16** List after inserting `newNode` at the end

We now repeat statements 1 through 6b three more times. Figure 17-17 shows the resulting list.