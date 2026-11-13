# Algorithm 8.2: SINSERT(list, key, Item)

+   1. Set p=list[head]
+   2. Loop for i=list[level] to 1 do
+      1. Loop while p->key[forward[i]]<key do
+         1. Set p=p->forward[i]
+         2. Set ip[i]=p
+      3. Set p=p->forward[i]
+   4. Check whether p[key]=key then
+      5. Set p[value]=Item
+   5. Else
+      1. Set |v|=rLevel()
+      2. Check whether |v|>list[level] then
+         1. Loop for i=list[level]+1 to |v| do
+            1. Set ip[i]=list[head]
+         2. Set list[level]=|v|
+         3. Set p=MakeNode(|v|, key, value)
+         4. Loop for i=1 to level do
+            1. Set p->forward[i]=ip[i]->forward[i]
+            2. Set ip[i]->forward[i]=p
+   6. End

# 8.3.4 Deletion

Deletion process also requires search for the key to delete the corresponding key-value pair. After identifying it the vector i.p points to the node that is before (left of) the deleting node. The link of the following node which was with the deleted node should be assigned to the node that was left to the deleted node. Algorithm 8.3 explains the deletion process.

# Algorithm 8.3: DELETE (list, key)

+   1. Set p=list[header]
+   2. Loop for i=list[level] to 1 do
+      Loop while p->forward[i] of key<key do
+      Set p[p->forward[i]]
+      Set ip[i]=p
+   3. Set p=p->forward[i]
+   4. Check whether p[key]=key then
+      Loop for i=1 to list[level] do
+      1. Check whether ip[i] of forward[i]!=p then
+      ii. Break
+      free(p)
+   5. Loop while list[list[level]>1 and list[header] of forward[list[level]]=NIL do
+      4. Set list[level]=list[level-1]
+      5. End

Algorithm 8.4 explains the random level generation.

# Algorithm 8.4: rlvel()

+   1. Set |v|=1
+   2. Loop while random()<r and |v|<MLevel do