```
}
else if (child->right != nullptr && child->right->color == RED)
{
    fix_double_red(child->right);
}
```

# Simple Tests

With such a complex implementation, it is extremely likely that some errors slipped in somewhere, and it is important to carry out thorough testing.

We can start with the test case used for the binary search tree from the book:

```
void test_from_book()
{
    RedBlackTree t;
    t.insert("D");
    t.insert("B");
    t.insert("A");
    t.insert("C");
    t.insert("F");
    t.insert("E");
    t.insert("I");
    t.insert("H");
    t.insert("M");
    t.insert("J");
    t.erase("A"); // Removing leaf
    t.erase("B"); // Removing element with one child
    t.erase("F"); // Removing element with two children
    t.erase("D"); // Removing root
    t.print();
    cout << "Expected: C E G H I J" << endl;
}
```

If this test fails (which it did for the author at the first attempt), it is fairly easy to debug. If it passes, it gives some confidence. But there are so many different configurations that more thorough tests are required.

For a more exhaustive test, we can insert all permutations of the ten letters A–J and check that the resulting tree has the desired contents. Here, we use the next_permutation function from the C++ standard library to visit all permutations of a string:

```
/**
Inserts all permutations of a string into a red-black tree and checks that
it contains the strings afterwards.
@param letters a sorted string of letters without repetition
@return the number of passing tests
*/

int insertion_test(string letters)
{
    int count = 0;
    string s = letters;
    do
    {
        RedBlackTree t;
        for (int i = 0; i < s.length(); i++)
        {
            t.insert(s.substr(i, 1));
        }
        bool pass = true;
        for (int i = 0; i < s.length(); i++)
        {

```