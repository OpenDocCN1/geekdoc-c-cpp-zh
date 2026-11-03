```
/* these are recursive calls */
/* insert the current node in the appropriate position, depending
on its value */
if (info < r->info)
    insert_node (r, r->left, info);
else
    insert_node (r, r->right, info);
}
```

Once the tree is created, it can be traversed in either of the tree ways discussed earlier (in-order, pre-order and post-order). The in-order traversal looks as follows.

```
void in_order (struct tree *root)
{
    /* if root does not exist, it means this is an empty tree. So, do not display anything */
    if (!root)
        return;

    in_order (root->left);
    print ("%d ", root->number);
    in_order (root->right);
}
```

Note that this also makes use of recursion. How does this program work? To understand this, refer to a sample tree shown in Fig. 16.3.

![](bbox=[0.28, 0.79, 0.73, 0.9])

Fig 16.3 Sample tree

First, the program checks if the root exists. In this case, the root (d) exists. So, the program proceeds.

It now calls itself, passing the left node of itself (i.e. b). Since this is a recursive call, it would enter the in_order function again, and call itself once again, passing the new left node of itself (i.e. a). This also being a recursive call, will result into a call to itself passing the new left node of itself (i.e. null, this time). This call to itself will now cause the if condition (to check if the root is null) will become true. Therefore, the recursion ends here. The functio8ns are now executed in the reverse order (i.e. with values a and b). This will print a and b.