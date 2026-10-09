```
public void Add(Song song) => list.Add(song);

public int Size => list.Count;
```

In this case, we even "changed" the property name (e.g., from Count to Size), which is not possible through inheritance. (Readers should be familiar with the modern, rather terse, C# syntaxes by now. The first one is easy. It is an "expression-bodied" method. What about the second one? Size is a "readonly" property (no setter). The getter returns list.Count.)

The only "limitation" of the composition-based code reuse is that we can only use public APIs of the embedded type. (Or, internal if it is in the same assembly.) In inheritance, we can reuse the parent class's protected members as well.

For the shuffle method, we (indirectly) rely on the List's indexers. The method implements the Fisher-Yates algorithm.

# ## 25.3. Sample Code Snippets - *shuffle-playlist*

We create a type Playlist to encapsulate the data, a list of songs, and to provide an API, in particular, the "Shuffle()" method. Here's the test driver for Playlist.