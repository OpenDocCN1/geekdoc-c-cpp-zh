```
1 vector<int> partialSum( const vector<int>& arr )
2 {
3     vector<int> result( arr.size() );
4
5     result[ 0 ] = arr[ 0 ];
6     for( int i = 1; i < arr.size(); ++i )
7         result[ i ] = result[ i - 1 ] + arr[ i ];
8
9     return result;
10 }
11
12 vector<int> vec;
13 ...
14 vector<int> sums = partialSum( vec ); // Copy in old C++; move in C++11
```

Figure 1.13 Returning of a stack-allocated rvalue in C++11

In addition to the return-by-value and return-by-constant-reference idioms, functions can use return-by-reference. This idiom is used in a few places to allow the caller of a function to have modifiable access to the internal data representation of a class. Return-by-reference in this context is discussed in Section 1.7.2 when we implement a simple matrix class.

# 1.5.5 std::swap and std::move

Throughout this section, we have discussed instances in which C++11 allows the programmer to easily replace expensive copies with moves. Yet another example of this is the implementation of a swap routine. Swapping doubles is easily implemented with three copies, as shown in Figure 1.14. However, although the same logic works to swap larger types, it comes with a significant cost: Now the copies are very expensive! However, it is easy to see that there is no need to copy; what we actually want is to do moves instead of copies. In C++11, if the right-hand side of the assignment operator (or constructor) is an rvalue, then if the object supports moving, we can automatically avoid copies. In other words, if vector<string> supports efficient moving, and if at line 10 x were an rvalue, then x could be moved into tmp; similarly, if y was an rvalue at line 11, then it could be moved in to y. vector does indeed support moving; however, x, y, and tmp are all lvalues at lines 10, 11, 12 (remember, if an object has a name, it is an lvalue). Figure 1.15 shows how this problem is solved; an implementation of swap at lines 1–6 shows that we can use a cast to treat the right-hand side of lines 10–12 as rvalues. The syntax of a static cast is daunting; fortunately, function std::move exists that converts any lvalue (or rvalue) into an rvalue. Note that the name is misleading: std::move doesn’t move anything; rather, it makes a value subject to be moved. Use of std::move is also shown in a revised implementation of swap at lines 8–13 of Figure 1.15. The swap function std::swap is also part of the Standard Library and will work for any type.