```
auto options_table = std::map<std::string, bool(*)(std::string const&)>
{{"debug"s, set_debug},
{"language"s, set_language}}; // Extend as appropriate

void parse_options_file(const char* filename) {
    auto options = std::ifstream(filename);
    if (!options.good()) return;
    while (!options.eof()) {
        auto key = std::string{};
        auto value = std::string{};
        options >> key >> value;
        auto fn = options_table.find(key);
        if (fn != options_table.end()) {
            (*(fn->second))(value);
        }
    }
}
```