```
template<typename... Types>
class PtrTuple : public Tuple<Types*...> {
    // extra operations provided only for PtrTuple
};

PtrTuple<int, float> t3; // Inherits from Tuple<int*, float*>
```