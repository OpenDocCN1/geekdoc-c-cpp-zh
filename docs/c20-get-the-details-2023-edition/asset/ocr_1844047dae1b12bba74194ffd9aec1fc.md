```
```cpp
}
}

int main() {

    std::cout << '\n';

    std::vector<int> myVec{0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
    std::string myStr{"Hello World"};

    printBoth(myVec, myStr, "Original containers");

    std::shift_left(std::begin(myVec), std::end(myVec), 2);
    std::shift_left(std::begin(myStr), std::end(myStr), 2);

    printBoth(myVec, myStr, "Shift left by 2");

    std::shift_right(std::begin(myVec), std::end(myVec), 2);
    std::shift_right(std::begin(myStr), std::end(myStr), 2);

    printBoth(myVec, myStr, "Shift right by 2");

    std::shift_right(std::begin(myVec), std::end(myVec), 20);
    std::shift_right(std::begin(myStr), std::end(myStr), 20);

    printBoth(myVec, myStr, "Shift right by 20 => no effect");

    std::cout << '\n';

}
```
```

In the program shiftLeftRight.cpp the std::vector and std::string are left-shifted by 2 (lines 28 and 29) and right-shifted by 2 (lines 33 and 34). The left shift operation by 2 puts the two last elements in a valid but unspecified state. Accordingly, the same holds for the right shift operation for the first two elements. The left shift operations in lines 38 and 39 have no effect because 20 is bigger than the size of the container.