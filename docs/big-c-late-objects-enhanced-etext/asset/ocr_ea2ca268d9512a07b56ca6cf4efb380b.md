![](bbox=[0.24, 0.16, 0.8, 0.34])

The following statement places a picture on the next row:

```
pic.add(pic2, 0, max_y + GAP);
```

Now we have written complete programs for all preliminary stages. We know how to line up the pictures, how to separate them with gaps, how to find out when to start a new row, and where to start it.

# EXAMPLE CODE

See sec09 of your companion code for the preliminary stages of the gallery program.

With this knowledge, producing the final version is straightforward. Here is the program listing.

# sec09/gallery6.cpp

```
```cpp
1 #include "picture.h"
2 #include <string>
3
4 using namespace std;
5
6 int main()
7 {
8     const int MAX_WIDTH = 720;
9     const int GAP = 10;
10    const string names = "abcdefghijklmnoprst";
11    const int PICTURES = names.length();
12
13    // Read the first picture
14    Picture pic("a.png");
15
16    // x and y are the top-left corner of the next picture
17    int x = pic.width() + GAP;
18    int y = 0;
19
20    // max_y is the largest y encountered so far
21    int max_y = pic.height();
22    for (int i = 1; i < PICTURES; i++)
23    {
24        // Read the next picture
25        Picture pic2(names.substr(i, 1) + ".png");
26        if (x + pic2.width() >= MAX_WIDTH) // The picture doesn't fit on the row
27        {
28            // Place the picture on the next row
29            x = 0;
30            y = max_y + GAP;
31        }
```
```