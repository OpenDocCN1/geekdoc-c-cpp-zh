```
if (nleft != nright)
{
    if (report_errors)
    {
        cout << "Left and right children of " << n->data
             << " have different black depths" << endl;
    }
    return -1;
}
if (n->parent == nullptr)
{
    if (!is_root)
    {
        if (report_errors)
        {
            cout << n->data << " is not root and has no parent" << endl;
        }
        return -1;
    }
    if (n->color != BLACK)
    {
        if (report_errors)
        {
            cout << "Root " << n->data << " is not black";
        }
        return -1;
    }
}
else
{
    if (is_root)
    {
        if (report_errors)
        {
            cout << n->data << " is root and has a parent" << endl;
        }
        return -1;
    }
    if (n->color == RED && n->parent->color == RED)
    {
        if (report_errors)
        {
            cout << "Parent of red " << n->data << " is red" << endl;
        }
        return -1;
    }
}
if (n->left != nullptr && n->left->parent != n)
{
    if (report_errors)
    {
        cout << "Left child of " << n->data
             << " has bad parent link" << endl;
    }
    return -1;
}
if (n->right != nullptr && n->right->parent != n)
{
    if (report_errors)
    {

```