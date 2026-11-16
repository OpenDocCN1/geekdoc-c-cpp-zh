```
```c
int channels = 0;
unsigned char* image = SOIL_load_image(
    fileName.c_str(),     // Name of file
    &mWidth,              // Stores width
    &mHeight,             // Stores height
    &channels,            // Stores number of channels
    SOIL_LOAD_AUTO        // Type of image file, or auto for any
);
```
```