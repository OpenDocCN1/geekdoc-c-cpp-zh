```
int filled_size = populate(rb);

if (check_red_black(rb, false)) // Found a valid tree
{
    string d = to_delete->data;
    rb.erase(d);
    bool pass = check_red_black(rb, true);
    for (int j = 0; j < filled_size; j++)
    {
        string s = "A";
        s[0] = s[0] + j;
        if (rb.count(s) == 0 && d != s)
        {
            cout << s << " deleted" << endl;
            pass = false;
        }
        if (rb.count(d) > 0)
        {
            cout << d << " not deleted" << endl;
            pass = false;
        }
        if (pass)
        {
            count++;
        }
        else
        {
            cout << "Failing tree: " << endl;
            print_detailed(rb.root, 0);
        }
    }
}
return count;
}
```

In our main function, we run all three tests. There are 3,628,800 insertion tests and 32 removal tests. (Of the 256 trees generated,224 are not valid red-black trees.) Because no error messages are displayed, we conclude that all tests pass.

```
int main()
{
    test_from_book();
    int passing = insertion_test("ABCDEFGHJI");
    cout << passing << " insertion tests passed." << endl;
    passing = removal_test(removal_test_template());
    cout << passing << " removal tests passed." << endl;
    return 0;
}
```

# worked_example_2/red_black_tree.h

```
1 #ifndef RED_BLACK_TREE_H
2 #define RED_BLACK_TREE_H
3
4 #include <string>
5
6 using namespace std;
7
```