node) of the list. The new value to be added in the list is added using tempnode→i_item; statement. The value in tempnode→ptr_next is set to NULL, indicating that now this node is the last node. The preserved starting address of the list is returned and accepted in the pointer variable head in the function main. Figure 6 illustrates insertion of a new element in the list:

![](bbox=[0.256, 0.23, 0.62, 0.342])

![](bbox=[0.247, 0.343, 0.815, 0.474])

![](bbox=[0.245, 0.475, 0.846, 0.585])

# ▲ Figure 6: Insertion of an Item in a Linked List

The second function displayitems in the program is defined to traverse and display the items in a list. Similar to the function additem, the pointer variable head, which contains address of the starting element of the list, is passed as an argument. It is accepted in the pointer variable tempnode. One by one, each node is traversed using while loop, and the items are displayed on the screen. Once a node is traversed, tempnode is advanced to the next location with tempnode=tempnode→ptr_next; statement. The loop continues till tempnode != NULL. The tempnode is set to NULL, when the tempnode points to the last node and the statement tempnode=tempnode→ptr_next; is executed.

The third function updateitem in the program is defined to update a value of an item. The old and new values of an item are accepted from the user with the function scanf. The list is then traversed till the old item is obtained. The tempnode pointer variable that initially contains address of the start of the list is used. The item contained in a tempnode→i_item is matched with the old value supplied by the user. If the match is successful, the old value is replaced by the new one; otherwise, the tempnode pointer is