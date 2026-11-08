This example will use any Box class that includes the operator<<(), which makes outputting Boxes to std::cout easier. We can remove the listBoxes() member of Truckload as well and add an overload for the << operator for outputting Truckload objects to a stream, analogous to that of the Box class. If you use the Truckload class that you created for Exercise 12-6 (the one which contains a nested Iterator class), you can implement this operator function without the need for a friend declaration. The definition for it then is as follows:

```
    std::ostream& operator<<(std::ostream& stream, const Truckload& load)
    {
        size_t count {};
        auto iterator = load.getIterator();
        for (auto box = iterator.getFirstBox(); box; box = iterator.getNextBox())
        {
            std::cout << *box << ' ';
            if (!(++count % 4)) std::cout << std::endl;
        }
        if (count % 4) std::cout << std::endl;
        return stream;
    }
```

You can use this to replace the listBoxes() member function of the old Truckload class. The code is similar to the listBoxes() code, except that now only public functions are used instead of directly working with the Packages in the list. The function uses the operator<<() function of the Box class. Outputting a Truckload object will now be very simple—you just use << to write it to cout.

If you add both the array subscript operator and the stream output operator to the Truckload class, you can use the following program to exercise these new operators:

```
    // Ex13_10.cpp
    // Using the subscript operator
    import <iostream>;
    import <memory>;
    import <crandom>;     // For random number generation
    import <functional>;  // For std::bind()
    import truckload;

    // Add the createUniformPseudoRandomNumberGenerator() function from Ex13_05 here.

    int main()
    {
        const double limit {99.0};      // Upper limit on Box dimensions
        auto random = createUniformPseudoRandomNumberGenerator(limit);

        Truckload load;
        const size_t boxCount {16};     // Number of Box object to be created

        // Create boxCount Box objects
        for (size_t i {}; i < boxCount; ++i)
            load.addBox(std::make_shared<Box>(random(), random(), random()));

        std::cout << "The boxes in the Truckload are:\n";
        std::cout << load;
    }
```