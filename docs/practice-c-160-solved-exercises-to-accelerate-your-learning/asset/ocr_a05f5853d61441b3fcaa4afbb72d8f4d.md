```
er","flow","flight\};

if (strs.empty()) {
    std::cout << "No common prefix" << std::endl;
    return 0;
}

// Take the shortest string as the potential prefix
std::string prefix = *min_element(strs.begin(), strs.end(), [](const std::string &s1, const std::string &s2) {
    return s1.size() < s2.size();
});

for (const std::string &str : strs) {
    // Compare the current prefix with each string in the list
    // If a mismatch is found, reduce the size of the prefix and try again
    while (str.substr(0, prefix.size())!= prefix) {
        prefix = prefix.substr(0, prefix.size() - 1);
        if (prefix.empty()) {
```