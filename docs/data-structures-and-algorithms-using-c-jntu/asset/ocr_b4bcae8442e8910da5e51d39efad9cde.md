4. While inserting the string "CAB", at first "C" will be searched at the root node.

+   a. Because "C" is available, move to the node "C".
+   b. At node "C", check for the node "A", because link to the node at "A" is not null, move in that path.
+   c. Check for the node "B", because the node, "B" is not available, the node "B" will be treated as a new node, and inserted under "A" as a branch node.

![](bbox=[0.15, 0.183, 0.903, 0.41])

Figure 15.4 Insertions of CAB and CAR

# Algorithm 15.5: Search (Trie T, String S)

+   1. Find the index of the node.
+      a. Index=ASCII Code S[0]
+   2. If length(S) and S[0]==\'\0\'
+      a. Return "STRING FOUND"
+   3. Else
+      a. If T->link[index]==NULL
+         i. Return "String Not Found".
+      b. Else /*Path Found, Follow the link*/
+         i. S++
+         ii. T->T->link[index]
+         iii. Search(T, S);

Search algorithm with an example: The search procedure takes the address of a trie (T) and a search string (S) as input arguments. Let a search string S="CAB" and trie (T) as the root node of Figure 15.4 b be considered, then the search procedure will be as below:

Pass 1: Checking for the node 'C'
S = "CAB" and
Trie T =

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | | 67 | | 255 |
|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | | | | 0 |

+   1. Find the index of the node.
+      Index = ASCII S[0]
+      = ASCII['C']
+      = 67