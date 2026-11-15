# Modify!

+   2. Add the following methods to the Pixel class:

```
void resetRed();
void resetGreen();
void resetBlue();
```

Each method should set the specified data member of the calling object to MAXVAL and reset the appropriate bit of overflowFlag.

+   3. Modify the output function

```
friend ostream& operator<<(ostream& out, const pixel& p)
```

so that the value of a pixel is output using colons, instead of whitespace, to separate the red, green and blue values.

+   4. Modify the input function

```
/*\n * Input >> operator. Expected pixel format is 100:150:100.\n */\nfriend istream& operator>>(istream& in, pixel& p)
```

to handle incorrect format by alerting the user and requesting new input. (Hint: Refer to error handling discussed in Chapter 5.)

# 10.3 Problem Solving Applied: Color Image Processing

The following is a picture of Io, one of Jupiter's moons, taken by the Galileo spacecraft:

![](bbox=[0.24, 0.69, 0.45, 0.88])

This image was downloaded from the nasa.gov home page following a search for Io images.