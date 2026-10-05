+   - list<ElementType>
The list is simpler than a vector and is very well suited for frequent insertions in the middle. However, the elements are not contiguous in memory but are internally linked. You do not have index access available. If you want to iterate over ranges, it is fast.

![](bbox=[0.331, 0.211, 0.668, 0.273])

**Figure 24.5** A "list" that can be traversed forwards and backward. Insertion is easy.

+   - forward_list<ElementType>
The exotic type mimics the fundamental structure of a linked list from C and requires minimal additional resources. However, it has a slightly different interface than all other containers. Every insertion works somewhat differently. Both list and forward_list are specialists in *splicing*—that is, transferring some consecutive or all elements from one list to another.

![](bbox=[0.331, 0.483, 0.668, 0.525])

**Figure 24.6** Elements of the "forward_list" only know their successor.

| Container | Description |
| --- | --- |
| array | Fixed size; similar to C-array ElementType[Size] |
| vector | All-rounder; similar to new ElementType[Size], but dynamically growing; inserting and removing at the back is very efficient |
| deque | Inserting and removing from the front and back is very efficient |
| list | Inserting everywhere is efficient; no [i]; forward and backward iterable |
| forward_list | Efficient insertion everywhere; low memory overhead; no [i]; no size(); only forward iterable |

**Table 24.4** Profiles of the sequence containers.

> Among the sequence-based container classes in C++, vector and array are the ubiquitous all-rounders.

# **24.6.1 Commonities and Differences**