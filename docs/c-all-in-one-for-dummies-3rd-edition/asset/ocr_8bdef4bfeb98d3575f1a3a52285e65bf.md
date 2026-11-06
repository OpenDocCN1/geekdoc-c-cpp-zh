# Listing 3-4 (continued)

```
```cpp
cout << "File: " << filename << endl;
bool done = false;
while (!done)
{
    infile >> num;
    if (infile.eof() == true)
    {
        done = true;
    }
    else
    {
        cout << num << endl;
    }
}
infile.close();
}

int main()
{
    ReadFile("../nums1.txt");
    ReadFile("../nums2.txt");
    return 0;
}
```
```

This listing is like Listing 3-2. However, instead of first reading a count, it just dives in and starts reading. The output of this example differs a little as a result. Here's what you get as output:

```
```
File: ../nums1.txt
100
101
102
103
104
File: ../nums2.txt
200
201
202
203
204
205

Process returned 0 (0x0)   execution time : 0.010 s
Press any key to continue.
```
```

![](bbox=[0.16, 0.726, 0.228, 0.792])

Note carefully how Listing 3-4 does its thing: The listing first *tries* to read in a number, and *then* it checks if it encountered an EOF. If you're familiar with other styles of reading in files, this approach may seem a little backwards to you. But that's the way the streams do it: First read, and if the read doesn't work, then abort.