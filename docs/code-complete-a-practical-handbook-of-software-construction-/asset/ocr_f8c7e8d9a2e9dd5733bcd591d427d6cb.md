# The Phony goto Debate

A primary feature of most goto discussions is a shallow approach to the question. The arguer on the “gotos are evil” side presents a trivial code fragment that uses gotos and then shows how easy it is to rewrite the fragment without gotos. This proves mainly that it’s easy to write trivial code without gotos.

The arguer on the “I can’t live without gotos” side usually presents a case in which eliminating a goto results in an extra comparison or the duplication of a line of code. This proves mainly that there’s a case in which using a goto results in one less comparison—not a significant gain on today’s computers.

Most textbooks don’t help. They provide a trivial example of rewriting some code without a goto as if that covers the subject. Here’s a disguised example of a trivial piece of code from such a textbook:

```
C++ Example of Code That’s Supposed to Be Easy to Rewrite Without gotos

do {
    GetData( inputFile, data );
    if ( eof( inputFile ) ) {
        goto LOOP_EXIT;
    }
    DoSomething( data );
} while ( data != -1 );
LOOP_EXIT:
```

The book quickly replaces this code with goto-less code:

```
C++ Example of Supposedly Equivalent Code, Rewritten Without gotos

GetData( inputFile, data );
while ( ( !eof( inputFile ) ) && ( ( data != -1 ) ) ) {
    DoSomething( data );
    GetData( inputFile, data )
}
```

This so-called “trivial” example contains an error. In the case in which data equals -1 entering the loop, the translated code detects the -1 and exits the loop before executing DoSomething(). The original code executes DoSomething() before the -1 is detected. The programming book trying to show how easy it is to code without gotos translated its own example incorrectly. But the author of that book shouldn’t feel too bad; other books make similar mistakes. Even the pros have difficulty translating code that uses gotos.

Here’s a faithful translation of the code with no gotos: