typedefs:

```
```cpp
typedef std::vector<int>        IntVector;
typedef std::vector<std::string> StringVector;

IntVector vi;
StringVector vs;
```
```

# 21.1 Defining class templates

Having covered the construction of function templates, we’re now ready for the next step: constructing class templates. Many useful class templates already exist. Rather than illustrating the construction of a class template by looking at an already existing class template the construction of another potentially useful new class template will be undertaken.

The new class implements a *circular queue*. A circular queue has a fixed number of `max_size` elements. New elements are inserted at its back and only its head and tail elements can be accessed. Only the head element can be removed from a circular queue. Once n elements have been appended the next element is inserted again at the queue’s (physical) first position. The circular queue allows insertions until it holds `max_size` elements. As long as a circular queue contains at least one element elements may be removed from it. Trying to remove an element from an empty circular queue or to add another element to a full circular queue results in exceptions being thrown. In addition to other constructors a circular queue must offer a constructor initializing its objects for `max_size` elements. This constructor must make available the memory for the `max_size` elements but must not call those elements default constructors (hinting at the use of the placement `new` operator). A circular queue should offer value semantics as well as a move constructor.

Please note that in the above description the actual data type that is used for the circular queue is nowhere mentioned. This is a clear indication that our class could very well be defined as a *class template*. Alternatively, the class could be defined for some concrete data type which is then abstracted when converting the class to a class template.

The actual construction of a class template is provided in the next section, where the class template `CirQue` (circular queue) is developed.

# 21.1.1 Constructing the circular queue: CirQue

The construction of a class template is illustrated in this section. Here, we’ll develop the class template `CirQue` (circular queue). This class template has one template type parameter, `Data`, representing the data type that is stored in the circular queue. The outline of the interface of this class template looks like this:

```
```cpp
template<typename Data>
class CirQue
{
    // member declarations
};
```
```

A class template’s definition starts like a function template’s definition:

+   - The keyword `template`, starting a template definition or declaration.
+   - The angle bracket enclosed list following `template`: a list containing one or more comma-separated elements is called the *template parameter list*. Template parameter lists may have multiple elements, like this:

```
```cpp
typename Type1, typename Type2, typename Type3
```
```