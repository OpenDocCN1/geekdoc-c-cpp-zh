```
size);
return false;
}
mFontData.emplace(size, font);
}
return true;
}
```

As with other resources, you want to keep track of loaded fonts in a central place. In this case, the Game class adds a map where the key is the filename of the font, and the value is a Font pointer. You then add a corresponding GetFont function. As with GetTexture and similar functions, GetFont first tries to find the data in its map and, if it fails, it loads the font file and adds it to the map.

The Font :: RenderText function, shown in Listing 11.3, creates a texture given a text string, using a font of the appropriate size. First, you convert the Vector3 color into an SDL_Color, where each component ranges from 0 to 255. Next, you look in the mFontData map to find the TTF_Font data corresponding to the font at the requested point size.

Next, you call the TTF_RenderText_Blended function, which takes in a TTF_Font*, the string of text