Remember that iterator is really a pointer to the map entry. And so we call find to determine if the item is inside the map entry. If it’s not, find returns `Flags.end()`. (That’s just the way the find function works. If we’d written the map class, we would have done things differently. Can you say simplify, simplify, simplify rather than obfuscate, obfuscate, obfuscate?)

And if we don’t get back `Flags.end()`, that means we found the item in the map. So in that case, we use `iterator->second` to obtain the value.

But notice what happens if we do get back `Flags.end()`, meaning the stream wasn’t found in the map. Then we just stick with the default value for `full`, which was true:

```
    bool full = true;
```

And so you can see that these output lines will function properly:

```
    cout << myoven << endl;
    cout << "============" << endl;
    cout << FullOvenInfo << myoven << endl;
    cout << "============" << endl;
    cout << MinOvenInfo << endl;
```

The first line with myoven line uses the default, which is a full listing. The second line with myoven says to definitely give us a full listing, using the `FullOvenInfo()` manipulator. And the third line with myoven gives a mini-mal listing, which we chose with the `MinOvenInfo()` manipulator.

Life is good.