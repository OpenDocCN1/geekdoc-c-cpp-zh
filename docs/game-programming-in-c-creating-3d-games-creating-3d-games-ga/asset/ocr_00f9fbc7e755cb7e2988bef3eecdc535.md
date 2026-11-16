```
// Create a vector of size + 1 (for null terminato
std::vector<char> bytes(static_cast<size_t>(fileSi
// Read in bytes into vector
file.read(bytes.data(), static_cast<size_t>(fileSi

// Load raw data into RapidJSON document
outDoc.Parse(bytes.data());
if (!outDoc.IsObject())
{
    SDL_Log("File %s is not valid JSON", fileName.c
    return false;
}

return true;
}
```

You then call LoadJSON at the start of LoadLevel:

Click here to view code image

```
rapidjson::Document doc;
if (!LoadJSON(fileName, doc))
```