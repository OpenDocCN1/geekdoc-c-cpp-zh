with the need to maintain the MAXSTK variable and consequently on the checking of OVERFLOW of the linked stack during a push operation.

# Procedure 6.3: PUSH_LINKSTACK(INFO, LINK, TOP, AVAIL, ITEM)

This procedure pushes an ITEM into a linked stack

+   1. [Available space?] If AVAIL = NULL, then Write OVERFLOW and Exit
+   2. [Remove first node from AVAIL list] Set NEW := AVAIL and AVAIL := LINK[AVAIL].
+   3. Set INFO[NEW] := ITEM [ Copies ITEM into new node]
+   4. Set LINK[NEW] := TOP [New node points to the original top node in the stack]
+   5. Set TOP = NEW [Reset TOP to point to the new node at the top of the stack]
+   6. Exit.

# Procedure 6.4: POP_LINKSTACK(INFO, LINK, TOP, AVAIL, ITEM)

This procedure deletes the top element of a linked stack and assigns it to the variable ITEM

+   1. [Stack has an item to be removed?] IF TOP = NULL then Write: UNDERFLOW and Exit.
+   2. Set ITEM := INFO[TOP] [Copies the top element of stack into ITEM ]
+   3. Set TEMP := TOP and TOP = LINK[TOP] [Remember the old value of the TOP pointer in TEMP and reset TOP to point to the next element in the stack]
+   4. [Return deleted node to the AVAIL list] Set LINK[TEMP] = AVAIL and AVAIL = TEMP.
+   5. Exit.

However, the condition TOP = NULL may be retained in the pop procedure to prevent deletion from an empty linked stack and the condition AVAIL = NULL to check for available space in the free-storage list.

# Example 6.4

Consider the linked stack shown in Fig. 6.7, the snapshots of the stack structure on execution of the following operations are shown in Fig. 6.10:

+   (i) Push BBB (ii) Pop (iii) Pop (iv) Push MMM

Original linked stack: