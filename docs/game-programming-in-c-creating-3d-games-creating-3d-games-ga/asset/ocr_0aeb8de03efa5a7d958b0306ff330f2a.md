```
```cpp
class Button
{
public:
    // Constructor takes in a name, font,
    // callback function, and position/dimensions of button
    Button(const std::string& name, class Font* font,
           std::function<void()> onClick,
           Vector2f pos, const Vector2f& dims);
    ~Button();

    // Set the name of the button, and generate name texture
    void SetName(const std::string& name);

    // Returns true if the point is within the button's bounds
    bool ContainsPoint(const Vector2f& pt) const;
    // Called when button is clicked
    void OnClick();

    // Getters/setters
    ...

private:
    std::function<void()> mOnClick;
    std::string mName;
    class Texture* mNameTex;
    class Font* mFont;
    Vector2f mPosition;
    Vector2f mDimensions;
    bool mHighlighted;
});
```
```