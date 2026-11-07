+   - inserting functions 214
+   - invalid state 94, 97
+   - invariant 92
+   - **IOStreams**
+     - move semantics 225
+   - is_nothrow_moveable<> 120
+   - is_nothrow_move_constructible<> 112, 120
+   - istream 225
+     - temporary 226
+   - **iterator**
+     - move_iterator 204

# J

+   - jthread 97, 227

# L

+   - **lambda**
+     - decltype(auto) 189
+     - deferred prefect returning 189
+     - perfect forwarding 151, 180
+     - perfect returning 189
+     - return type 189
+     - template parameters 151
+   - lvalue 125, 232
+     - check for 138

# M

+   - make_move_iterator() 204
+   - make_pair() 219
+   - materialize 129
+   - **member**
+     - and std::move() 130
+     - for moved-from state 202
+     - initialization 61
+     - invalid moved-from state 97
+     - pointers 102
+     - references 102
+     - value category 130
+     - with disabled move semantics 54
+   - **member function**
+     - called with std::forward<> 146
+     - called with std::move() 82

+   - with reference qualifier 86
+   - **member type**
+     - reference 159, 160
+     - Meyers
+       - on move-only types 195
+   - motivation 3
+   - **move()** 27
+     - and const 22
+     - as static_cast 28
+     - calling member functions 82
+     - change value category 135
+     - compiler warnings 61
+     - for functions 130
+     - for members 130
+     - header file 27
+     - impossible to avoid 60
+     - in return statement 81
+     - moved-from objects 28
+     - reuse the object 29
+     - self-move 45
+     - to itself 30
+     - valid but unspecified state 28, 92
+     - versus forward<> 164
+     - with disabled move semantics 54
+   - **move() algorithm** 199
+     - **move assignment**
+       - and noexcept 118
+       - broken 39
+       - container guarantees 213
+       - generated 56
+       - implementation 44
+       - operator 56
+       - self-move 45
+       - to itself 30
+   - **move_backward() algorithm** 199
+   - **move constructor** 55
+     - and noexcept 118
+     - broken 39
+     - container guarantees 213
+     - =default 51
+     - =delete 52
+     - for strings 20
+     - generated 55
+     - implementation 42
+     - noexcept 107, 110