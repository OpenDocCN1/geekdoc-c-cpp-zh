enable_if_class.cpp:87:7: error: no viable overloaded '&='
v2&= 7.0; // not enabled
~~^ ~~
enable_if_class.cpp:6:44: note: candidate template ignored:
disabled by 'enable_if' [with U = double]
using enable_if_t = typename std::enable_if<Cond, T>::type;