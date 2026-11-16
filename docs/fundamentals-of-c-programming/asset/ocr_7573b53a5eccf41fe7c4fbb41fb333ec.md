# 17.7. PROTECTED MEMBERS

```
// Draw a rectangle using text graphics
void draw() const {
    // Access the inherited protected fields
    int rows = static_cast<int>(length + 0.5),
        columns = static_cast<int>(width + 0.5);
    // Draw the rectangle
    for (int r = 0; r < rows; r++) {
        for (int c = 0; c < columns; c++)
            std::cout << '*';
        std::cout << '\n';
    }
}
int main() {
    DrawableRectangle rec1(3, 2),
        rec2(10, 5),
        rec3(4, 8);
    rec1.draw();
    std::cout << "--------------------\n";
    rec2.draw();
    std::cout << "--------------------\n";
    rec3.draw();
}
```

Listing 17.32 (drawablerectangle.cpp) displays

![](bbox=[0.12, 0.51, 0.8, 0.78])

The DrawableRectangle::draw method needs access to the fields length and width to be able to draw the rectangle. It is important to remember that every DrawableRectangle object contains these fields because it inherits them from Rectangle; however, if the length and width fields were declared private instead of protected in Rectangle, DrawableRectangle::draw would not be able to access these fields.