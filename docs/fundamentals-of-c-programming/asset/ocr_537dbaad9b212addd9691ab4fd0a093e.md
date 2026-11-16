```
```cpp
// Print the body of the n x n multiplication table
void print_contents(int n) {
    for (int current_row = 1; current_row <= n; current_row++)
        print_row(current_row, n);
}

// Print a multiplication table of size n x n.
void timetable(int n) {
    // First, print column heading
    col_header(n);

    // Print table contents
    print_contents(n);
}

// Forces the user to enter an integer within a
// specified range first is either a minitmum or maximum
// acceptable value last is the corresponding other end
// of the range, either a maximum or minitmum value
// Returns an acceptable value from the user
int get_int_range(int first, int last) {
    // If the longer number is provided first,
    // switch the parameters
    if (first > last) {
        int temp = first;
        first = last;
        last = temp;
    }

    // Insist on values in the range first...last
    std::cout << "Please enter a value in the range "
              << first << "..." << last << ": ";
    int in_value; // User input value
    bool bad_entry;
    do {
        std::cin >> in_value;
        bad_entry = (in_value < first || in_value > last);
        if (bad_entry) {
            std::cout << in_value << " is not in the range "
                      << first << "..." << last << '\n';
            std::cout << "Please try again: ";
        }
    } while (bad_entry);

    // in_value at this point is guaranteed to be within range
    return in_value;
}

int main() {
    // Get table size from user; allow values in the
    // range 1...18.
    int size = get_int_range(1, 18);

    // Print a size x size multiplication table
    timetable(size);
}
```
```