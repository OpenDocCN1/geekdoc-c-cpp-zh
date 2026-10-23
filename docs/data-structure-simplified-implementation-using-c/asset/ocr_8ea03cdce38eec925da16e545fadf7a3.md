```
break;
else
r=r->left;
}
else
{
if(r->rthread==1)
{
newnode->left=r->left;
r->lthread=0;
newnode->lthread=1;
newnode->right=r->right;
newnode->rthread=1;
r->rthread=0;
break;
}
else
r=r->right;
}      //end of else
}// end of while
```

# 8.5 TRAVERSAL IN A THREADED TREE

Traversal in threaded tree is a complex procedure. It requires variety of factors to be considered during traversal. Since, thread of a child may connects to the root therefore, cycle will be formed that will result in an infinite loop. Therefore, due care need to be exercised to prevent this infinite looping.

In the ordinary BST, during traversal we are only examine the presence of NULL where we terminate the traversal. Similarly, in the threaded tree, we continue to head till thread is not encountered. Inorder traversal in the inthreaded tree is depicted as follows:

```
void thread::inorder()
{
tNode *r=root;
in_order(r);
}
void thread::in_order(tNode *root) // start of in order threaded function
```