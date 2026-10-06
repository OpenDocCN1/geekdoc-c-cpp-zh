
# Solutions to Chapter 2 | Linked Lists

## 2.2 Implement an algorithm to find the nth to last element of a singly linked list.

### SOLUTION

Note: This problem screams recursion, but we will do it in a different way because it's trickier. In a question like this, expect follow up questions about the advantages of recursion vs iteration.

Assumption: The minimum number of nodes in list is n.

Algorithm:

- 1. Create two pointers, p1 and p2, that point to the beginning of the node.
- 2. Increment p2 by n-1 positions, make it point to the nth node from the beginning (to make the distance of n between p1 and p2).
- 3. Check for p2->next == null if return value of p1, otherwise increment p1 and p2. If next of p2 is null it means p1 points to the nth node from the last as the distance between two is n.
- 4. Repeat Step 3.

```
LinkedListNode nthToLast(LinkedListNode head, int n) {
  if (head == null || n < 1) {
    return null;
  }
  LinkedListNode p1 = head;
  LinkedListNode p2 = head;
  for (int j = 0; j < n - 1; ++j) { // skip n-1 steps ahead
    if (p2 == null) {
      return null; // not found since list size < n
    }
    p2 = p2.next;
  }
  if (p2 == null) {
    return null;
  }
  while (p2.next != null) {
    p1 = p1.next;
    p2 = p2.next;
  }
  return p1;
}
```

# Solutions to Chapter 2 | Linked Lists

## 2.3 Implement an algorithm to delete a node in the middle of a single linked list, given only access to that node.

### EXAMPLE

Input: the node `c` from the linked list a->b->c->d->e

Result: nothing is returned, but the new linked list looks like a->b->d->e

### SOLUTION

The solution to this is to simply copy the data from the next node into this node and then delete the next node.

> NOTE: This problem cannot be solved if the node to be deleted is the last node in the linked list. That’s ok—your interviewer wants to see you point that out. You could consider marking it as dummy in that case. This is an issue you should discuss with your interviewer.

```
public static boolean deleteNode(ListNode n) {
    if (n == null || n.next == null) {
        return false; // Failure
    }
    ListNode next = n.next;
    n.data = next.data;
    n.next = next.next;
    return true;
}
```

# Solutions to Chapter 2 | Linked Lists

## 2.4 You have two numbers represented by a linked list, where each node contains a single digit. The digits are stored in reverse order, such that the 1's digit is at the head of the list. Write a function that adds the two numbers and returns the sum as a linked list.

### EXAMPLE

Input: (3 -> 1 -> 5), (5 -> 9 -> 2)

Output: 8 -> 0 -> 8

### SOLUTION

We can implement this recursively by adding node by node, just as we would by digit.

- 1. result.data = (node1 + node2 + any carry) % 10
- 2. if node1 + node2 > 10, carry a 1 to the next addition.
- 3. add the tails of the two nodes, passing along the carry.

```
LinkedList addLists(ListNode l11, ListNode l12,
    int carry) {
    ListNode result = new ListNode(carry, null, null);
    int value = carry;
    if (l11 != null) {
        value += l11.data;
    }
    if (l12 != null) {
        value += l12.data;
    }
    result.data = value % 10;
    if (l11 == null || l12 == null || value >= 10) {
        ListNode more = addLists(l11 == null ? null : l11.next,
            l12 == null ? null : l12.next,
            value >= 10 ? 1 : 0);
        result.setNext(more);
    }
    return result;
}
```

# Solutions to Chapter 2 | Linked Lists

## 2.5 Given a circular linked list, implement an algorithm which returns the beginning of the loop.

### DEFINITION

Circular linked list: A linked list in which a node's next pointer points to an earlier node, making a loop.

### EXAMPLE

Input: A -> B -> C -> D -> E

Output: C

### SOLUTION

If we move two pointers, one with speed 1 and another with speed 2, they will meet if the linked list has a loop. Why? Think about two cars on a track—the faster car will always pass the slower one! The tricky part here is finding the start of the loop. Imagine two people racing around a track, one running twice as fast as the other. If they start at the same place, when will they next meet? They will meet k nodes before the start (Fast Runner would have made k + (n - k) steps, including its start, and Slow Runner would have made n - k steps).

Now, going back to the problem, Fast Runner (n2) and Slow Runner (n1) are moving around our circular list, n2 will have a head start on the loop. Specifically, it will have a head start of k nodes, where k is the number of nodes before the loop. Since n2 has a head start of k nodes, n1 and n2 will meet k nodes before the start.

So we now know the following:

- 1. Head is k nodes from LoopStart (by definition).
- 2. MeetingPoint for n1 and n2 is k nodes from LoopStart (as shown).

Thus, if we move n1 back to Head and keep n2 at MeetingPoint, and move both at the same pace, they will meet at LoopStart.

```
LinkedList FindBeginning(LinkedListNode head) {
    ListNode n1 = head;
    ListNode n2 = head;

    // Find meeting point
    while (n2.next != null) {
        n1 = n1.next;
        n2 = n2.next.next;
        if (n1 == n2) {
            break;
        }
    }

    // Error check - there is no meeting point, therefore no loop
    if (n2.next == null) {
        return null;
    }

    /* Move n1 to Head. Keep n2 at Meeting Point. Each are k steps
     * from Loop Start. If they move at same pace, they must
     * meet at LoopStart. */
    while (n1 != n2) {
        n1 = n1.next;
        n2 = n2.next;
    }

    // Now n2 points to the start of loop
    return n2;
}
```

# Solutions to Chapter 3 | Stacks and Queues

## 3.1 Describe how you could use a single array to implement three stacks.

### SOLUTION

Approach 1:

Divide the array in three parts and allow the individual stack to grow in that limited space (note: "[" inclusive, ")" means exclusive of the end point).

- for stack 1, we will use [0, n/3)
- for stack 2, we will use [n/3, 2n/3)
- for stack 3, we will use [2n/3, n)

This solution is based on the assumption that we do not have extra information about the usage of space by individual stacks and that we can't modify or use any extra space. With these constraints, we are left with no other choice but divide equally.

```
int stackSize = 300;
int[] buffer = new int[stackSize * 3];
int[] stackPointer = {0, 0, 0}; // stack pointers to top elem
void push(int stackNum, int value) {
    /* Find the index of the top element in the array + 1,
       * increment the stack pointer */
    int index = stackNum * stackSize + stackPointer[stackNum] + 1;
    stackPointer[stackNum]++;
    buffer[index] = value;
}
int pop(int stackNum) {
    int index = stackNum * stackSize + stackPointer[stackNum];
    stackPointer[stackNum]--;
    int value = buffer[index];
    buffer[index] = 0;
    return value;
}
int peek(int stackNum) {
    int index = stackNum * stackSize + stackPointer[stackNum];
    return buffer[index];
}
boolean isEmpty(int stackNum) {
    return stackPointer[stackNum] == stackNum * stackSize;
}
```

Approach 2:

In this approach, any stack can grow as long as there is any free space in the array.

We sequentially allocate space to the stacks and we link new blocks to the previous block. This means any new element in a stack keeps a pointer to the previous top element of that particular stack.

In this implementation, we face a problem of unused space. For example, if a stack deletes some of its elements, the deleted elements may not necessarily appear at the end of the array. In that case, we would not be able to use these newly freed spaces.

To overcome this deficiency, we can maintain a free list and the whole array space would be given initially to the free list. For every insertion, we would delete an entry from the free list. In case of deletion, we would simply add the index of the free cell to the free list.

In this implementation we would be able to have flexibility in terms of variable space utilization but we would need to increase the space complexity.

```
int stackSize = 300;
int indexUsed = 0;
int[] stackPointer = {-1, -1, -1};
StackNode[] buffer = new StackNode[stackSize * 3];
void push(int stackNum, int value) {
    int lastIndex = stackPointer[stackNum];
    stackPointer[stackNum] = indexUsed;
    indexUsed++;
    buffer[stackPointer[stackNum]] = new StackNode(lastIndex, value);
}
int pop(int stackNum) {
    int value = buffer[stackPointer[stackNum]].value;
    int lastIndex = stackPointer[stackNum];
    stackPointer[stackNum] = buffer[stackPointer[stackNum]].previous;
    buffer[lastIndex] = null;
    indexUsed--;
    return value;
}
int peek(int stackNum) { return buffer[stackPointer[stackNum]].value; }
boolean isEmpty(int stackNum) { return stackPointer[stackNum] == -1; }
class StackNode {
    public int previous;
    public int value;
    public StackNode(int p, int v) {
    value = v;
    previous = p;
    }
}
```
