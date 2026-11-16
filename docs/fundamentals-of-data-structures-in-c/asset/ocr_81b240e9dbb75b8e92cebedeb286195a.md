```
tree *delNoChild(tree *btree, tree *par, tree *loc)
{
if(par == NULL)
return NULL;
else if(loc == par->left)
par->left = NULL;
else if(loc == par->right)
par->right = NULL;
return btree;
}
```

```
tree *delOneChild(tree *btree, tree *par, tree *loc)
{
tree *temp;
if(loc->left != NULL)
temp = loc->left;
else
temp = loc->right;
if(par == NULL)
btree = temp;
else if(loc == par->left)
par->left = temp;
else if(loc == par->right)
par->right = temp;
return btree;
}
```

```
tree *delTwoChild(tree *btree, tree *par, tree *loc)
{
tree *suc, *parSuc;
parSuc = loc;
for(suc = loc -> right; suc->left != NULL;suc = suc->left)
parSuc = suc;
if(suc->left==NULL && suc->right==NULL)
delNoChild(btree, parSuc, suc);
else
delOneChild(btree, parSuc, suc);
if(par == NULL)
btree = suc;
else if(loc == par->left)
par->left = suc;
else if(loc == par->right)
par->right = suc;
```