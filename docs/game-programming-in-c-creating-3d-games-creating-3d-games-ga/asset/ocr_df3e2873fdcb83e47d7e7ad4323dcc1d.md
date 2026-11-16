Font::Load function, shown in Listing 11.2, first creates a vector of the desired point sizes, and then it loops over this vector, calling TTF_OpenFont once per size and adding each TTF_Font to the mFontData map.

# Listing 11.2 Font::Load Implementation

Click here to view code image

```
bool Font::Load(const std::string& fileName)
{
    // Support these font sizes

    std::vector<int> fontSizes = {
        8, 9, 10, 11, 12, 14, 16, 18, 20, 22, 24, 26, 2
        30, 32, 34, 36, 38, 40, 42, 44, 46, 48, 52, 56,
        60, 64, 68, 72
    };

    // Call TTF_OpenFont once per every font size
    for (auto& size : fontSizes)
    {
        TTF_Font* font = TTF_OpenFont(fileName.c_str(),
        if (font == nullptr)
        {
            SDL_Log("Failed to load font %s in size %d",
```