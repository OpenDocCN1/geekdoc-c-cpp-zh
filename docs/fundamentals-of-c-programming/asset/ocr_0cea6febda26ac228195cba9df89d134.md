```
~LogComparator();
};
```

```
// Method that actually performs the comparison
// Derived classes may override this method
template <typename T>
bool LogComparator<T>::compare_impl(const T& m, const T& n) {
    fout << "Comparing " << m << " to " << n << '\n';
    // Base class method does the comparison
    return Comparator<T>::compare_impl(m, n);
}
```

```
// Method that actually performs the swap
// Derived classes may override this method
template <typename T>
void LogComparator<T>::swap_impl(T& m, T& n) {
    fout << "Swapping " << m << " and " << n << '\n';
    //T temp = m;
    //m = n;
    //n = temp;
    // Base class method does the swap
    Comparator<T>::swap_impl(m, n);
}
```

```
// The client must initialize a LogComparator object with a
// suitable comparison function and the file name of the
// text file to receive logging messages.
template <typename T>
LogComparator<T>::LogComparator(bool (*f)(const T&, const T&),
                                const std::string& filename): Comparator<T>(f) {
    fout.open(filename);
    if (!fout.good()) {
        std::cout << "Could not open log file " << filename
                  << " for writing\n";
        exit(1); // Terminate the program
    }
    // fout is an instance variable, not a local variable,
    // so the file stays open when the constructor finishes
}
```

```
template <typename T>
LogComparator<T>::~LogComparator() {
    fout.close();
}
```

```
int main() {
    // Make a vector of integers
    // vector<int> vec = { 23, -3, 10, 4, 215, 0, -3, 2 };
    std::cout << "Before: ";
    print(std::begin(vec), std::end(vec));
    std::cout << '\n';
    LogComparator<int> lt(less_than<int>, "upsort.log");
}
```