```
// https://godbolt.org/z/9943MfExc
#include <vector>
class Image {
  std::vector<char> data;
  public:
    void load(const char* filename); // loads image data
};
class Screen {
  public:
    void show(Image& image); // N image should be const
  };
void paint(Screen&screen, const Image& image) {
    screen.show(image);
  }
};
int main() {
  Image image;
  image.load("peter.png");
  Screen screen;
  paint(screen, image);
}
```

**Listing 4.15** The compiler helps to write correct programs by checking the types.

The omission of “the power of 2” in C++ corresponds perhaps to a missing const: the screen Screen has a method show with which it paints an image. You would think that the image image would not be changed when painting. It is therefore likely that the type of the show parameter should have been const Image& rather than Image&.

A forgotten const alone is not yet critical, mind you. But what would happen if someone “accidentally” placed the call image.load("paul.png"); in the show method? That would change the image. This cannot happen with the const parameter: the compiler reports an error.