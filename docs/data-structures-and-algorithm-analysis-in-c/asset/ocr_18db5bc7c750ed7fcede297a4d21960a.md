The first two symbols are operands, so we create one-node trees and push pointers to them onto a stack.²

![](bbox=[0.426, 0.153, 0.703, 0.283])

Next, a + is read, so two pointers to trees are popped, a new tree is formed, and a pointer to it is pushed onto the stack.

![](bbox=[0.426, 0.365, 0.732, 0.552])

Next, c, d, and e are read, and for each a one-node tree is created and a pointer to the corresponding tree is pushed onto the stack.

![](bbox=[0.426, 0.642, 0.732, 0.822])

Now a + is read, so two trees are merged.