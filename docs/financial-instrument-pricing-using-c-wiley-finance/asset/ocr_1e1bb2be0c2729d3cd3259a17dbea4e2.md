```
void Rotate()
{
    // II. Rotations
    std::cout << "\n*** Block II, Rotate ***\n";
    // Rotating elements in a sequence
    using namespace boost::assign;
    std::vector<int> myVec = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
    print(myVec, "input vector");

    //std::cout << "Choose size of offset to right: "; int offset;
    // std::cin >> offset;
    int offset = 3;

    offset = std::abs(offset);
    std::rotate(myVec.begin(), myVec.begin() + offset, myVec.end());
    print(myVec, std::string("Modifier, vector rotated "));

    // Rotate with copy
    std::multiset<int> mySet = { 11, 22, 33, 44, 55, 66, 77, 88, 99 };
    std::cout << "Input multiset: ";
    for (auto el : mySet)
    {
        std::cout << el << ",";
    }
    std::cout << '\n';
    std::multiset<int>::iterator pos = mySet.begin();
    std::advance(pos, offset);    // increment the position of an iterator

    std::vector<int> vecOut;
    std::rotate_copy(mySet.begin(), pos, mySet.end(),
                     std::back_inserter(vecOut));
    print(vecOut, std::string("Selector, set rotated "));

    // Rotate from position having a given value
    std::multiset<int>::iterator posValue = mySet.find(55);
    vecOut.clear();

    std::rotate_copy(mySet.begin(), posValue, mySet.end(),
                     std::back_inserter(vecOut));
    print(vecOut, std::string("Selector, set rotated: "));
}
```

The output is:

```
**** Block II, Rotate ****
input vector: 1, 2, 3, 4, 5, 6, 7, 8, 9,
Modifier, vector rotated : 4, 5, 6, 7, 8, 9, 1, 2, 3,
Input multiset: 11,22,33,44,55,66,77,88,99,
Selector, set rotated : 44, 55, 66, 77, 88, 99, 11, 22, 33,
Selector, set rotated: : 55, 66, 77, 88, 99, 11, 22, 33, 44,
```