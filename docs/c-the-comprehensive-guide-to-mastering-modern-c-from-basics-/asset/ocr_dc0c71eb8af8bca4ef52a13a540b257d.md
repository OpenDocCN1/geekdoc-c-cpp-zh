```
std::formatter<std::string> sub_fmt {
    constexpr auto sub_fmt::parse(std::format_parse_context& pctx) {
        return pctx.parse(pctx); // returns iterator to '}'
    }
    auto format(const Elf& elf, std::format_context& fctx) const {
        std::string s = std::format("{}: {}, {}, {}, {}",

            elf.name, elf.folk, elf.birth_year, elf.era);
        return sub_fmt.format(s, fctx); // delegate formatting
    }
};
int main() {
    std::vector<Elf> elves = {
        {"Feanor", 1169, "First Age", "Noldor"},
        {"Galadriel", 1362, "EZ", "Noldor"},
        {"Legolas", 87, "DZ", "Sindar"},
        {"Elrond", 532, "EZ", "Half-elf"},
        {"Elwe", 1050, "EZ", "Sindar"},
    };
    for (const auto& e : elves) {
        std::cout << std::format("Elf: {:20}", e) << std::endl;
    }
}
```

# Listing 27.31 A formatter can delegate the parsing of format

Here I have delegated the parsing of format attributes and the formatting of the output to the standard std::string to sub_fmt. Therefore, I need to somehow generate a string in string s that contains the std::format and I make this easy for myself by building a string with std::format and passing it to sub_fmt.

The output looks like this for Feanor: 

Elf: Feanor/Nordor (1169 EZ)

If you need more sophisticated formatting, you have to parse the format attributes yourself. When parsing, assume that you have an iterator at pctx.begin() pointing to the first character after the bracket { or after