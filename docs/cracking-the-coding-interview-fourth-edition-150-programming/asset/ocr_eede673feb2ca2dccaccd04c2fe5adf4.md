# Solutions to Chapter 2 | Linked Lists

2.1 Write code to remove duplicates from an unsorted linked list.

FOLLOW UP
How would you solve this problem if a temporary buffer is not allowed?

# SOLUTION

If we use a buffer, we can keep track of elements in a hashtable and remove any dups:

```
public static void deleteDups(ListNode n) {
    Hashtable table = new Hashtable();
    ListNode previous = null;
    while (n != null) {
        if (table.containsKey(n.data)) previous.next = n.next;
        else {
            table.put(n.data, true);
            previous = n;
        }
        n = n.next;
    }
}
```

Without a buffer, we can iterate with two pointers: "current" does a normal iteration, while "runner" iterates through all prior nodes to check for dups. Runner will only see one dup per node, because if there were multiple duplicates they would have been removed already.

```
public static void deleteDups2(ListNode head) {
    if (head == null) return;
    ListNode previous = head;
    ListNode current = head.next;
    while (current != null) {
        ListNode runner = head;
        while (runner != current) { // Check for earlier dups
            if (runner.data == current.data) {
                ListNode tmp = current.next; // remove current
                current.next = tmp;
                previous = tmp;
                current = tmp; // update current to next node
                break; // all other dups have already been removed
            }
            runner = runner.next;
        }
        if (runner == current) { // current not updated - update now
            previous = current;
            current = current.next;
        }
    }
}
```