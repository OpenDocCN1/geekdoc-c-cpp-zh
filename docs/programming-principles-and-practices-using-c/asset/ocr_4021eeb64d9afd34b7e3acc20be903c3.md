the `?`. Until we see the `+` we might be on our way to reading `1.55555`. So, we need a “stream” that produces a token when we ask for one using get() and where we can put a token back into the stream using putback(). Everything we use in C++ has a type, so we have to start by defining the type Token_stream.

You probably noticed the public: in the definition of Token in §6.3.3. There, it had no apparent purpose. For Token_stream, we need it and must explain its function. A C++ user-defined type often consists of two parts: the public interface (labeled public:) and the implementation details (labeled private:). The idea is to separate what a user of a type needs for convenient use from the details that we need in order to implement the type, but that we’d rather not have users mess with:

```
```cpp
class Token_stream {
 public:
    // user interface
 private:
    // implementation details
    // (not directly accessible to users of Token_stream)
};
```
```

Obviously, users and implementers are often just us “playing different roles,” but making the distinction between the (public) interface meant for users and the (private) implementation details used only by the implementer is a powerful tool for structuring code. The public interface should contain (only) what a user needs, which is typically a set of functions. The private implementation contains what is necessary to implement those public functions, typically data and functions dealing with messy details that the users need not know about and shouldn’t directly use.

Let’s elaborate the Token_stream type a bit. What does a user want from it? Obviously, we want get() and putback() functions – that’s why we invented the notion of a token stream. The Token_stream is to make Tokens out of characters that it reads for input, so we need to be able to make a Token_stream and to define it to read from cin. Thus, the simplest Token_stream looks like this:

```
```cpp
class Token_stream {
 public:
    Token get();            // get a Token
    void putback(Token t);  // put a Token back
 private:
    // implementation details
};
```
```

That’s all a user needs to use a Token_stream. Experienced programmers will wonder why cin is the only possible source of characters, but we decided to take our input from the keyboard. We’ll revisit that decision in a Chapter 7 exercise.