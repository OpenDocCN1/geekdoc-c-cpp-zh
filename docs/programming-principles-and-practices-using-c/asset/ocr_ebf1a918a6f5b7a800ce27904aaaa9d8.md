```
while (true) {
    cin >> n;
    if (cin) {                // we got an integer; now check it
        if (1<=n && n<=10) break;
        cout << "Sorry "
             << n << " is not in the [1:10] range; please try again\n";
    }
    else if (cin.fail()) {   // we found something that wasn't an integer
        cin.clear();          // set the state back to good();
                              // we want to look at the characters
        cout << "Sorry, that was not a number; please try again\n";
        for (char ch; cin>>ch && !isdigit(ch); )  // throw away non-digits
            /* nothing */ ;
        if (!cin) error("no input");    // we didn't find a digit; give up
        cin.unget();      // put the digit back, so that we can read the number
    }
    else {
        error("no input");        // eof or bad: give up
    }
}
// if we get here n is in [1:10]
```

This is messy, and rather long-winded. In fact, it is so messy that we could not recommend that people write such code each time they needed an integer from a user. On the other hand, we do need to deal with the potential errors because people do make them, so what can we do? The reason that the code is messy is that code dealing with several different concerns is all mixed together:

+   - Reading values
- Prompting the user for input
- Writing error messages
- Skipping past “bad” input characters
- Testing the input against a range

The way to make code clearer is often to separate logically distinct concerns into separate functions. For example, we can separate out the code for recovering after seeing a “bad” (i.e., unexpected) character:

```
void skip_to_int()
{
    if (cin.fail()) {          // we found something that wasn't an integer
        cin.clear();          // we'd like to look at the characters
```