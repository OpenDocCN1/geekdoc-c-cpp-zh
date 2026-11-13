```
#define maxchar 3 /* Key is formed using 3 letters p,
q, r only */
#define max_key_length 5
class trieNode
{
    public:
        TrieNode *branch[maxchar];
        TrieData *dataptr;
};
typedef char key[max_key_length];
// SearchTrie() searches for the data starting from
// the root.
// If found, returns corresponding dataptr, otherwise
// returns null
TrieNode *SearchTrie(TrieNode *root, Key data)
{
    int p;
    for(p = 0; p < max_key_length&&root!=null; p++)
    {
        if(data[p]=='\0')
            break;
        /* data found, and root is pointing to the
        node having pointer to data */
        else
            root = root->branch[data[p] - 'p'];
    }
    if(root != null && root->dataptr == null)
        return null;
    return root;
}
```

# 13.3.5 Splay Tree

Of the many other variations on balanced binary trees, perhaps the most intriguing are the splay trees, introduced by Sleator and Tarjan, which are self-adjusting.

Splay trees are a form of BSTs. A splay tree maintains a balance without any explicit balance condition such as colour. Instead, 'splay operations', which involve rotations, are performed within the tree every time an access is made. The amortized cost of each operation on an n-node tree is O(log,n). One application of splay trees simplifies dynamic trees.