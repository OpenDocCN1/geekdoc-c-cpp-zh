```
template<typename... Types>
class MyTuple : public Tuple<Types...> {
    // extra operations provided only for MyTuple
};

MyTuple<int, float> t2;  // inherits from Tuple<int, float>
```