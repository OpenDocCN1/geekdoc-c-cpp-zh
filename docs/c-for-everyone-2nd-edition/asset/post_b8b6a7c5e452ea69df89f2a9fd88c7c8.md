
```cpp
stream >> x;
return x;
}

/**
 * Extracts the country and associated value from an input line.
 * @param line a line containing a country name, followed by a number
 * @param country the string for holding the country name
 * @param value the variable for holding the associated value
 * @return true if a line has been read, false at the end of the stream
 */
void read_line(string line, string& country, double& value)
{
    int i = 0; // Locate the start of the first digit
    while (!isdigit(line[i])) { i++; }
    int j = i - 1; // Locate the end of the preceding word
    while (isspace(line[j])) { j--; }

    country = line.substr(0, j + 1); // Extract the country name
    value = string_to_double(line.substr(i)); // Extract the number value
}

int main()
{
    ifstream in1;
    ifstream in2;
    in1.open("worldpop.txt"); // Open input files
    in2.open("worldarea.txt");

    ofstream out;
    out.open("world_pop_density.txt"); // Open output file
    out << fixed << setprecision(2);

    string line1;
    string line2;

    // Read lines from each file
    while (getline(in1, line1) && getline(in2, line2))
    {
        string country;
        double population;
        double area;

        // Split the lines into country and associated value
        read_line(line1, country, population);
        read_line(line2, country, area);

        // Compute and print the population density
        double density = 0;
        if (area != 0) // Protect against division by zero
        {
            density = population * 1.0 / area;
        }
        out << setw(40) << left << country
            << setw(15) << right << density << endl;
    }

    return 0;
}
```

### WORKED EXAMPLE 8.1 Looking for Duplicates

This Worked Example processes a file to locate lines that contain repeated words.

## 8.6 Random Access and Binary Files

In the following sections, you will learn how to read and write data at arbitrary positions in a file, and how to edit image files.

### 8.6.1 Random Access

> You can access any position in a random access file by moving the file pointer prior to a read or write operation.

So far, you’ve read from a file an item at a time and written to a file an item at a time, without skipping forward or backward. That access pattern is called sequential access. In many applications, we would like to access specific items in a file without first having to read all preceding items. This access pattern is called random access (see Figure 3). There is nothing “random” about random access—the term means that you can read and modify any item stored at any location in the file.

Only file streams support random access; the cin and cout streams, which are attached to the keyboard and the terminal, do not. Each file stream has two special positions: the get position and the put position (see Figure 4). These positions determine where the next character is read or written.

The following function calls move the get and put positions to a given value, counted from the beginning of the stream.

```cpp
strm.seekg(position);
strm.seekp(position);
```

To determine the current values of the get and put positions (counted from the beginning of the file), use

```cpp
position = strm.tellg();
position = strm.tellp();
```

![](img/23fb3582e93ebc95909e1de029c3d388_399_0.png)

![](img/23fb3582e93ebc95909e1de029c3d388_399_1.png)

At a sit-down dinner, food is served sequentially. At a buffet, you have “random access” to all food items.

![](img/23fb3582e93ebc95909e1de029c3d388_400_0.png)

### 8.6.2 Binary Files

Many files, in particular those containing images and sounds, do not store information as text but as binary numbers. The numbers are represented as sequences of bytes, just as they are in the memory of the computer. (Each byte is a value between 0 and 255.) In binary format, a floating-point number always occupies 8 bytes. We will study random access with a binary file format for images.

We have to cover a few technical issues about binary files. To open a binary file for reading and writing, use the following command:

```cpp
fstream strm;
strm.open(filename, ios::in | ios::out | ios::binary);
```

You read a byte with the call

```cpp
int input = strm.get();
```

This call returns a value between 0 and 255. To read an integer, read four bytes b₀, b₁, b₂, b₃ and combine them to b₀ + b₁ · 256 + b₂ · 256² + b₃ · 256³. We will supply a helper function for this task.

The >> operator cannot be used to read numbers from a binary file.

### 8.6.3 Processing Image Files

In this section, you will learn how to write a program for editing image files in the BMP format. Unlike the more common GIF, PNG, and JPEG formats, the BMP format is quite simple because it does not use data compression. As a consequence, BMP files are huge and you will rarely find them in the wild. However, image editors can convert any image into BMP format.

There are different versions of the BMP format; we will only cover the simplest and most common one, sometimes called the 24-bit true color format. In this format, each pixel is represented as a sequence of three bytes, one each for the blue, green, and red value. For example, the color cyan (a mixture of blue and green) is 255 255 0, red is 0 0 255, and medium gray is 128 128 128.

A BMP file starts with a header that contains various pieces of information. We only need the following items:

| Position | Item |
|---:|---|
| 2 | The size of this file in bytes |
| 10 | The start of the image data |
| 18 | The width of the image in pixels |
| 22 | The height of the image in pixels |

To try out this program, take one of your favorite images, use an image editor to convert to BMP format (or use queen-mary.bmp from the code files for this book), then run the program and view the transformed file in an image editor. Exercises P8.21 and P8.22 ask you to produce more interesting effects.

**ch08/imagemod.cpp**

```cpp
1  #include <iostream>
2  #include <fstream>
3  #include <cstdlib>
4
5  using namespace std;
6
7  /**
8     Processes a pixel by forming the negative.
9     @param blue the blue value of the pixel
10    @param green the green value of the pixel
11    @param red the red value of the pixel
12  */
13 void process(int& blue, int& green, int& red)
14 {
15    blue = 255 - blue;
16    green = 255 - green;
17    red = 255 - red;
18 }
19
20 /**
21    Gets an integer from a binary stream.
22    @param stream the stream
23    @param offset the offset at which to read the integer
24    @return the integer starting at the given offset
25 */
26 int get_int(fstream& stream, int offset)
27 {
28    stream.seekg(offset);
29    int result = 0;
30    int base = 1;
31    for (int i = 0; i < 4; i++)
32    {
33       result = result + stream.get() * base;
34       base = base * 256;
35    }
36    return result;
37 }
38
39 int main()
40 {
41    cout << "Please enter the file name: ";
42    string filename;
43    cin >> filename;
44
45    fstream stream;
46    // Open as a binary file
47    stream.open(filename.c_str(), ios::in | ios::out | ios::binary);
48
49    int file_size = get_int(stream, 2); // Get the image dimensions
50    int start = get_int(stream, 10);
51    int width = get_int(stream, 18);
52    int height = get_int(stream, 22);
// Scan lines must occupy multiples of four bytes
int scanline_size = width * 3;
int padding = 0;
if (scanline_size % 4 != 0)
{
    padding = 4 - scanline_size % 4;
}

if (file_size != start + (scanline_size + padding) * height)
{
    cout << "Not a 24-bit true color image file." << endl;
    return 1;
}

stream.seekg(start); // Go to the start of the pixels

for (int i = 0; i < height; i++) // For each scan line
{
    for (int j = 0; j < width; j++) // For each pixel
    {
        int pos = stream.tellg(); // Go to the start of the pixel

        int blue = stream.get(); // Read the pixel
        int green = stream.get();
        int red = stream.get();

        process(blue, green, red); // Process the pixel

        stream.seekg(pos); // Go back to the start of the pixel

        stream.put(blue); // Write the pixel
        stream.put(green);
        stream.put(red);
    }

    stream.seekg(padding, ios::cur); // Skip the padding
}

return 0;
}
```

## SELF CHECK

- 25. In plain English, what does the following code segment do?

    ```cpp
    strm.seekg(0);
    strm.put(0);
    ```

- 26. How would you modify the `imagemod.cpp` program to flip the green and blue values of each pixel for a psychedelic effect?

- 27. What happens if you run the `imagemod.cpp` program twice on the same image file?

- 28. Could we have implemented the image modification program with sequential access only? If not, why not?

- 29. Suppose a BMP file stores a 100 x 100 pixel image in BMP format, with the image data starting at offset 64. What is the total file size?

**Practice It** Now you can try these exercises at the end of the chapter: R8.12, R8.13, P8.21.
