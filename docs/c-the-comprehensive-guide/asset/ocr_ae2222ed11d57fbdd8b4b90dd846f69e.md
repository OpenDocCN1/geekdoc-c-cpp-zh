```
```cpp
cout << val << " ";
cout << "\n";
}
```
```

**Listing 12.35** When you enrich “auto” with &, you get a modifiable reference.

The first auto must be enriched with & so that you get a reference to the actual data that you want to modify with val *= 2. If you had only written for(auto val : data)—without &—then val would have been a copy each time, and val *= 2; would have had no effect on the content of data.

For the second auto, it is quite okay because you do not need to modify val for the output. And because you want to make sure that this does not happen accidentally, you can protect yourself from unintended changes by enriching with const. Thus, each element is copied to val, marked as constant, and output.

For int, this copy is fine. However, if the elements were immensely large and expensive to copy, you should have combined both enrichments. Assuming Image is a class that is expensive to copy, it would be advisable to use const and & together with auto:

```
```cpp
vector<Image> data{ Image{"Monalisa.png", "TheScream.png"} };
for(const auto& image : data)
    show(image);
```
```

Returning to the original example, there are a few lines left where auto could not be used:

```
```cpp
vector_t huge{ 12ULL, 1000000000ULL, 9ULL, 0ULL, };
// ...
set sorted( huge.begin(), huge.end() );
```
```

For huge, you cannot use auto because the compiler needs to know that you want to declare a vector<unsigned long long>. The compiler might guess the element type from the 12ULL list elements, but whether you want a vector, set, or something else entirely, the compiler cannot know.

Whenever you initialize a list in curly brackets, you must explicitly specify the desired type. If you were to use auto here, the declared variable would get the internal initializer_list<> type, which is usually not what you want.

The same applies to sorting: you do not have a single expression from which the compiler can deduce the type, but an explicit constructor call (with two iterators as arguments). In such a case, the compiler must already know from which class you want to call the constructor. This is not an initialization with a left side and a right side as auto would need to be able to do its job.

But the compiler helps you as much as it can. Since C++17, the compiler automatically determines the type parameter for set from the constructor arguments—without you