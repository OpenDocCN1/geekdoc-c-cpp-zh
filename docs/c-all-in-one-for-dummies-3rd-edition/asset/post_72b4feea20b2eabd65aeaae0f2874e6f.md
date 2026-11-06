
# Book V
## Chapter 3: Reading with Input Streams

```cpp
}
outfile << start + i << endl;
}
outfile.close();
}

int main()
{
    WriteFile("../nums1.txt", 5, 100);
    WriteFile("../nums2.txt", 6, 200);
    return 0;
}
```

You can see that this application writes two files. This example places the files in your /CPP_AIO/BookV/Chapter 03 folder. The .. path refers to the parent folder of the current folder, which is /CPP_AIO/BookV/Chapter 03/FileRead02. The reason we're giving a path is that the next listing reads from the files, and we want to make sure that the application can find the files. Using the parent folder also avoids problems with newer operating systems that don't allow root directory access, such as Windows 7, OS X, and Linux.

Note that the WriteFile() function takes a filename, a count, and a start. It uses this information to write a series of numbers to the file. But before it writes those numbers, it writes the count, like this:

```cpp
    outfile << count << endl;
```

Then it uses a loop to write count numbers to the file.

And, of course, when the WriteFile() function is all done, it closes the file. _Good application, good._

The FileRead03 example shown in Listing 3-2 is an example of how to read this data back in.

### Listing 3-2: Using Code to Open a File and Read It Back In

```cpp
#include <iostream>
#include <fstream>
#include <string>

using namespace std;

void ReadFile(string filename)
{
    ifstream infile(filename.c_str());
    int count;
    int i;
    int num;
    cout << "File: " << filename << endl;
    infile >> count;
    cout << "This file has " << count << " items." << endl;
    for (i=0; i<count; i++)
    {
        infile >> num;
        cout << num << endl;
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

You can see in Listing 3-2, like Listing 3-1, `filename` includes the path names for the files the application is reading in.

Now look at the `ReadFile()` function. This function opens the file and then immediately reads in a number. This number represents the number of items to read in. It’s the first number that was written by the `WriteFile()` function in the previous listing, Listing 3-1.

As the writer of both the application that writes the file and the application that reads the file, we agreed (both sides of us agreed, that is, or so we think) on the format of the file both for reading it and for writing it. And by sticking to this format, we can assure ourselves that we can read in the file that we previously wrote. When you run this application, you’ll see the following output.

![](img/6ba99460b0feb3585671a4612ff5fabb_667_0.png)

```text
File: /MyData/nums1.txt
This file has 5 items.
100
101
102
103
104
File: /MyData/nums2.txt
This file has 6 items.
200
201
202
203
204
205

Process returned 0 (0x0)    execution time : 0.000 s
Press any key to continue.
```

Now another possibility for reading and writing a file is that you continue reading data from the file until you reach the end of the file. How do you do this? You test the `istream` or `ifstream` object for the EOF.

Listings 3-3 and 3-4 show you how you can do this. As with the earlier listings, the first writes a couple of files, and the second reads them in.

First, Listing 3-3 shows the `FileRead04` example.

### Listing 3-3: Using Code to Write to a File but Not Record a Count

```cpp
#include <iostream>
#include <fstream>
#include <string>

using namespace std;

void WriteFile(string filename, int count, int start)
{
    ofstream outfile(filename.c_str());
    int i;
    for (i=0; i<count; i++)
    {
        outfile << start + i << endl;
    }
    outfile.close();
}

int main()
{
    WriteFile("../nums1.txt", 5, 100);
    WriteFile("../nums2.txt", 6, 200);
    return 0;
}
```

As you can probably see, Listing 3-3 is like Listing 3-1, except Listing 3-3 does not start out by writing out a count.

The `FileRead05` example in Listing 3-4 reads the numbers back in.

### Listing 3-4: Reading from a File and Looking for the EOF Condition

```cpp
#include <iostream>
#include <fstream>
#include <string>

using namespace std;

void ReadFile(string filename)
{
    ifstream infile(filename.c_str());
    int num;
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

This listing is like Listing 3-2. However, instead of first reading a count, it just dives in and starts reading. The output of this example differs a little as a result. Here's what you get as output:

```text
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

![](img/6ba99460b0feb3585671a4612ff5fabb_669_0.png)

Note carefully how Listing 3-4 does its thing: The listing first *tries* to read in a number, and *then* it checks if it encountered an EOF. If you're familiar with other styles of reading in files, this approach may seem a little backwards to you. But that's the way the streams do it: First read, and if the read doesn't work, then abort.

Therefore, you have to have some strange logic in your code. Here's the general algorithm:

```text
set done to false
while not done
    read a number
    if encounter an end of file
        set done to true
    else
        process the number read in
    end-if
end-while
```

Something bothers us about this approach: We need a big if statement, and the process the number part goes in an else block. We like having a Boolean variable called done, because then we can use a while loop that reads like this:

```cpp
while (!done) // pronounced "while not done"
```

If lots of processing is needed, the processing will all be piled inside the else portion of the if block. And that can get ugly with a million indentations. In this case, check for EOF and then break out of the loop, like this:

```cpp
if (infile.eof() == true)
    break;
```

But if you do that, you have no reason for the done variable. So what do you put in the while loop? A lot of people do this:

```cpp
while (1)
{
    infile >> num;
    if (infile.eof() == true)
        break;
    cout << num << endl;
}
```

Yes, they put while (1). In other words, the while loop spins forever until a break statement comes along. We're not particularly fond of the while (1) construct because it's a bit counterintuitive for our little tiny brains, but a lot of people do it; and we have to admit that we like the short if statement, just breaking if the EOF is true. You choose which method you want to use. And heck, you may even be able to dream up a couple more ways to do this.

### Reading Various Types

Reading a file is fun, but it can get complicated when you want to read spaces. Suppose we have these two strings that we want to write to a file:

> "That's the steak by the poodle that I'll have for dinner."
>
> "I will have the Smiths for dinner, too."

Nothing earth-shattering there. Reading it in is pretty easy, too; you just use the getline() function in the ifstream or istream class. The catch is that the getline() function wants a character array, not a string object. So go ahead and read it into a character array, and then convert it to a string object like so:

```cpp
char buf[1024];
infile.getline(&buf[0], 1024);
string str(buf);
```

![](img/6ba99460b0feb3585671a4612ff5fabb_672_0.png)

You don't have to convert the array to a string object; if you want, you can just work with the character array. But we prefer to work with string objects because they're instances of classes and you get all kinds of nice member functions that can manipulate the strings. We're all about making our lives easier.

The ReadString01 example in Listing 3-5 shows how to write the strings with a delimiter. You can see that this has nothing particularly magical about it (other than the quantum physics involved in running the microprocessor, but we don't care about that).

### Listing 3-5: Writing Strings with a Delimiter Is Easy

```cpp
#include <iostream>
#include <string>
#include <fstream>

using namespace std;

void WriteString(ofstream &file, string words)
{
    file << words;
    file << ",";
}

int main()
{
    ofstream delimfile("../delims.txt");

    WriteString(delimfile, "This is a dog");
    WriteString(delimfile, "Some dogs bite");
    WriteString(delimfile, "Some dogs don't bite");
    WriteString(delimfile, "Humans that is");
    WriteString(delimfile, "All dogs bite");
    WriteString(delimfile, "Food that is");
    WriteString(delimfile, "I say, food food food.");

    delimfile.close();
    return 0;
}
```
