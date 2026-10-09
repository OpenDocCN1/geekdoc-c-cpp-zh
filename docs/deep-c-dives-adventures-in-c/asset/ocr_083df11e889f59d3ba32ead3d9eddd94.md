You can count the number of characters in the literal and simply set the array to the correct size or you could let the compiler do it for you:
`char myString[] = "Hello World";`
as myString has a final `NULL` element it might be one bigger than you expect based on a simple character count.
What makes `NULL`-terminated strings so nice to work with is that you can scan them using a `for` loop. For example, you can find out how many characters are in a string using:
`for(int i=0; myString[i]; i++) count++;`
Notice the use of `myString[i]` as the stopping condition. Another good reason for using `NULL` as the sentinel, is that it is also interpreted as `false`. This gives you some idea of why `NULL`-terminated strings seemed such a good idea back in the early days of `C`. It also indicates why they aren’t quite so good – you have to scan the entire string to find its length and what happens if there isn’t a `NULL`.
You may not be careless enough to write loops that might not end, but there is still the problem of using such a thing within a library function. For example, the standard function `strlen` returns the length of a string and seems innocent enough, but it uses the same sort of `for` loop to scan the string and to count characters. If there is no `NULL` then the loop doesn’t end and you overrun the end of the array. Notice that the `sizeof` operator will tell you the length of the array that holds the string i.e. `sizeof(string)`. This returns at once and doesn’t scan the string so it is 100% safe.
Nearly all of the standard string handling functions have this defect. There is a much safer version of each of these functions indicated by an “n” in the middle of the name. For example:
`strnlen(str, size);`
will return the length of str as long as it is less than size. That is, the scan stops after size characters have been examined and no NULL found. The only problem is that this is not a standard C function. It’s a Posix standard, i.e. part of Linux/Unix.
Similarly the function:
`strcpy(dest,src);`
will copy the string in `src` into `dest` including the final `NULL`. A safe version is:
`strncpy(dest,src,size);`
which stops after `size` characters if it hasn’t encountered a `NULL` in `src` before this. Its behavior is slightly more dangerous than you might think in that if `src` doesn’t have a `NULL` in its first `size` bytes then `dest` will not be