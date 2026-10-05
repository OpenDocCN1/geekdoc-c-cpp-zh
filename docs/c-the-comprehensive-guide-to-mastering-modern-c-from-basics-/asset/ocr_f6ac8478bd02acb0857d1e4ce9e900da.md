# 22.6 The Main Program

The conclusion is then formed by main() from
Listing 22.4. You will not encounter any surprises. You
need to close the anonymous namespace opened in the
first listing, then main begins.

A comprehensive try-catch handles any exceptions that
you might have thrown elsewhere in the program.
exc.what() outputs an appropriate error message.

The fName vector stores all command-line arguments,
which the for loop then iterates over. In it, pack() calls
the compression function.

```
// https://godbolt.org/zSbW x6PzdP
// namespace
int main(int argc, const char* argv[]) {
    try {
        const std::vector<std::string> fName{argv+1, argv+argc};
        for(auto fName : fName) {
            std::cout << "packing " << fName << " ...";
            pack(fName, fName+".gz");
            std::cout << fName << ".gz" << "\n";
        }
    } catch (std::runtime_error &exc) {
        std::cerr << "Error: " << exc.what() << "\n";
    }
}
```

**Listing 22.4** With "main" in "gzippack.cpp", the example is complete.