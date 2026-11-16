For example, if the original dictionary contained only five words:

```
can<LF>
canal<LF>
cancel<LF>
cancer<LF>
candid<LF>
```

it would be compressed as follows:

```
0can<LF>
3al<LF>
3cel<LF>
5r<LF>
3did<LF>
```

In the encoded version of the dictionary, only those letters appear which do not occur successively in the previous word. The number in front of the trailing end of each word represents the number of characters that are the same. Decoding demands sequential reading so that the preceding word is once again available. The count preceding the word to be decompressed provides the number of leading characters to be retained and the unencoded characters are then concatenated.

In the preceding example, the original dictionary contains 31 characters and the compressed version contains 22, for a space savings of 29%. Additional compression can be realized by reducing the number of newline characters, <LF>, at the end of each line. This can be achieved by outputting the words on one line until a predefined right margin is reached:

```
0can3al3cel5r3did<LF>
```

The compressed dictionary now contains 18 characters for a space savings of 42%. In practice, though, entries in an actual dictionary will be much closer to each other, lexicographically speaking, than those in this example, and the savings greater. With a larger dictionary, the compression ratio exceeds 50%.