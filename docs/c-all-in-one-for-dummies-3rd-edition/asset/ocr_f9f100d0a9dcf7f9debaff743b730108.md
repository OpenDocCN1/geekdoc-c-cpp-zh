# ## What's a protocol?

Okay, we're going to give you a list of numbers: 1600 20500 1849 20240. Go ahead and use them the way we intend you to use them, and then send us back the answer, at which point we'll send you our response. What's that? You're not sure what we want you to do with them? Aha! You need a protocol. As defined in this chapter, a protocol is simply a rule for how data is ordered. A protocol in general defines rules for exchanging information of any sort between computers (think of it as a diplomatic role). The two systems negotiate the exchange of data based on standardized rules.

As it happens, the first number in the set of numbers we provided is the street address of the White House in Washington, DC, and the second number is the zip code for the White House. The third number is the street address of the main office for the National Park Service headquarters, and the fourth is the National Park Service zip code. Of course, you probably didn't realize that (unless you happen to work for the Park Service and recognized parts of your address!).

But now suppose you tell us, 'Send me the White House street address, then its zip code, then the National Park Service street address, and then its zip code.' Then we would go ahead and send the four numbers to you. At that point, we wouldn't have any need to send a bunch of extra information, such as English words describing what each number is. If we give them to you in the exact order you requested them, that will be all you need. In fact, if you're writing a computer application that receives this information and we pad it with other information, such as descriptions, your application may not be equipped to handle all that info, and you have a problem. In other words, our application and your application must agree on a protocol. A protocol dictates the order of the information and how it's formatted. Further, a protocol dictates how you'll respond. You may send back a single number 1, which means that you received the data properly, and we may send a single 0, which means that you'll be getting no further information. That's a protocol, and protocols are useful when reading data, whether it's from a file or over the Internet.

You can easily read in these numbers with the following code. First, make sure you add #include <fstream> (but not fstream.h, as you'll pick up an old, outdated, yucky file) as well as #include <iostream>. And you probably will need the line using namespace std; if you're using a newer compiler and library.

It's important to define some variables to hold the data you want to read. These variables (found in the FileRead01 example) will work fine:

```
    string weight;
    string height;
    string width;
    string depth;
```