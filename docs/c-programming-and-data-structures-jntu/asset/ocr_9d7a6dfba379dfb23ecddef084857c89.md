# The following function, insert_node builds a sorted binary tree.

```
struct tree *insert_node (struct tree *root, /* root of the tree */
struct tree *r, /* node to be inserted */
int info /* value of the node that is being inserted */)
{
  /* this is non-recursive portion of the code */

  /* if node to be inserted does not exist, create it */
  if (!r)
  {
    r = (struct tree *) malloc (sizeof (struct tree));

    if (!r)
    {
      printf ("Insufficient memory\n.");
      return;
    }

    /* set the left-right pointers of r to null, and set
       its information to that received from the calling
       function
    */
    r->left = NULL;
    r->right = NULL;
    r->info = info;

    /* root does not exist, so this is the first entry */
    if (!root)
      return r; /* r becomes the root now */

    /* if the value of the node to be inserted is less than
       that of the root, insert it before the root */
    if (info < root->info)
      root->left = r;
    else
      /* if the value of the node to be inserted is greater than
         that of the root, insert it after the root */
      root->right = r;

    return r;
  }
}
```