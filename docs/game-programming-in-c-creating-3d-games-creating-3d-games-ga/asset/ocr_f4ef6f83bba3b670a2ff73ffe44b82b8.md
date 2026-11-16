```
void LevelLoader::SaveLevel(Game* game,
    const std::string& fileName)
{
    // Create the document and root object
    rapidjson::Document doc;
    doc.SetObject();

    // Write the version
    JsonHelper::AddInt(doc.GetAllocator(), doc, "version", LevelVersion);

    // Create the rest of the file (TODO)
    // ...

    // Save JSON to string buffer
    rapidjson::StringBuffer buffer;
    // Use PrettyWriter for pretty output (otherwise use Writer)
    rapidjson::PrettyWriter<rapidjson::StringBuffer> writer(buffer);
    doc.Accept(writer);
    const char* output = buffer.GetString();

    // Write output to file
    std::ofstream outFile(fileName);
    if (outFile.is_open())
    {
        outFile << output;
    }
}
```