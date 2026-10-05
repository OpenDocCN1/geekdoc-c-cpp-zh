```
array pics{Picture("Mona"), Picture("Scream"), Picture("Vincent")};
std::cout << pics[0].name() << '\n'; // Output: Mona
// enlarge
Picture new_pic = append(move(pics), "Clocks");
auto more = append(move(pics), new_pic);
// after
std::cout << pics[0].name() << '\n'; // Output: 
std::cout << more[0].name() << '\n'; // Output: Mona
std::cout << more[3].name() << '\n'; // Output: Clocks
}
```

# ### Listing 2.2 You get back an array enlarged by one element.

First, let me explain what happened in main(). In the middle, you see a call to append. It is important here that you pass both arguments to move; otherwise, the append function could not move the data out of its parameters. As a reminder: with std::move, you convert an lvalue reference into an rvalue reference—and tell the compiler that it is allowed to “steal” the data from the argument. If you omit this, you still get a larger array back, but the original pics and new_pic parameters would remain unchanged. However, the data was moved out of them, which you can see by the fact that pics[0].name() is empty. Also, pics[0].data is empty.

You still have three Picture elements in pics, but they are all empty and are now in the first three slots of the array<Picture,4> named more.

How did that happen? The key lies in the helper function help_append and in index_sequence. First, append calls the helper function:

```
return help_append(move(data), move(elem), std::make_index_sequence<S>
```