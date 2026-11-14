In such a case, we should ask ourselves whether we can restructure our software so that such obscure implementations are realized once, in a dark corner of a library, and everywhere else we write clear and simple statements such as:

```
A = B * C;
```

as program and not as pseudo-code. This is one of the main goals of this book: to show you how to write the short expression you want while the implementation under the hood squeezes out the maximal performance.

Another frequent usage of comments is to remove snippets of code temporarily to experiment with alternative implementations, e.g.:

Click here to view code image

```
for ( ... ) {
    // int x = a + b + c
    int x = a + d + e;
    for ( ... ) {
    ...
```

Like C, C++ provides a form of block comments, surrounded by /* and */. They can be used to render an arbitrary part of a code line or multiple lines into a comment. Unfortunately, they cannot be nested: no matter how many levels of comments are opened with /*, the first */ ends all block comments. Many programmers run into this trap sometimes: they want to comment out a longer fraction of code that already contains a block comment so that the comment ends earlier than intended, for instance:

Click here to view code image

```
for ( ... ) {
    /* int x87y97= yo6954fq;       // start new comment
    int x78y98= yo6953fq;
    /* int x78y99= yo6952fq;       // start old comment
    int x78y9a= yo6951fq;  */      // end old comment
    int x78y9b= yo6950fq;  */      // end new comment
(presumably)
    int x78y9c= yo6949fq;
    for ( ... ) {
```

Here, the line for setting x78y9b should have been disabled, but the preceding /* terminated the comment prematurely.