```
```cpp
        std::cout << gen2.getNextValue() << " ";
    }

    std::cout << "\n\n";

    std::vector myVec{1, 2, 3, 4, 5};
    auto gen3 = getNext(myVec);
    for (int i = 0; i < myVec.size(); ++i) {
        std::cout << gen3.getNextValue() << " ";
    }

    std::cout << '\n';

}
```
```

In this example, the generator is instantiated and used three times. In the first two cases, `gen` (line 76) and `gen2` (line 83) are initialized with `std::string helloWorld`, while `gen3` uses a `std::vector<int>` (line 91). The output of the program should not be surprising. Line 78 returns all characters of the string `helloWorld` successively, line 85 only the first five characters, and line 93 the elements of the `std::vector<int>`.

You can try out the program on the Compiler Explorer³.

![](bbox=[0.371, 0.551, 0.626, 0.646])

A generator successively returning each element

To make it short. The implementation of the `Generator<T>` is almost identical to the previous one. The crucial difference with the previous program is the coroutine `getNext`.

# ## getNext

```
```cpp
template <typename Cont>
Generator<typename Cont::value_type> getNext(Cont cont) {
    for (auto c: cont) co_yield c;
}
```
```

`getNext` is a function template that takes a container as an argument and iterates in a range-based for loop through all container elements. After each iteration, the function template pauses. The return type `Generator<typename Cont::value_type>` may look surprising to you. `Cont::value_type` is

³https://godbolt.org/z/jozmva