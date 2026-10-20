
While you as the implementer always retain the expedient option of refining a requirement without engaging your customer, my experience indicates that this path invariably leads to rewriting the code repeatedly: once for what you thought the user wanted, once for what the user thought he wanted, and once for what the user actually wanted.

Obviously, for our case study, we only have a hypothetical end user, so we’ll simply do the refinement ourselves. We specify the following:

- 1. The CLI should accept a text command for any command defined for the calculator (those that exist in the command repository plus undo, redo, help, and exit).
- 2. The help command should display a list of all available commands and a short explanatory message.
- 3. The CLI should accept space-separated commands in the order in which they should be processed.

Recall that this order corresponds to Reverse Polish Notation. All commands on a line are processed after return is pressed.

- 4. After commands are processed, the interface should display at most the top four elements of the stack plus the stack’s current size.

Surprisingly, the minimal requirements listed above are sufficient to build a simple CLI. While these requirements are somewhat arbitrary, something specific needed to be chosen in order to describe a design and implementation. If you don’t like the resultant CLI, I highly encourage you to specify your own requirements and modify the design and implementation accordingly.

## The CLI Design

The design of the CLI is remarkably simple. Because our overall architectural design placed the entire “business logic” of the calculator in the back end, the front end is merely a thin layer that does nothing more than accept and tokenize input from the user, pass that input to the controller sequentially, and display the results. Let’s begin by describing the interface.

### The Interface

From the analysis we performed earlier in the chapter, we know that the concrete CLI class will inherit from the abstract UserInterface class. This inheritance is public because the CLI “is a” UserInterface and must substitute as one. Hence, the CLI must implement the UserInterface’s two abstract pure virtual functions, postMessage() and stackChanged(). These two methods are only called polymorphically through a UserInterface reference; therefore, both methods become part of the private interface of the CLI. Other than construction and destruction, the only functionality that the CLI needs to expose publicly is a command that starts its execution. This function drives the entire CLI and only returns (normally) when the user requests to quit the program. Combining the above, the entire interface for the CLI can be given by the code in Listing 5-4.

**Listing 5-4. The Entire Interface for the CLI**

```
class Cli : public UserInterface
{
    class CliImpl;
public:
    Cli(istream& in, ostream& out);
    ~Cli();

    void execute(bool suppressStartupMessage = false, bool echo = false);

private:
    void postMessage(const string& m) override;
    void stackChanged() override;

    unique_ptr<CliImpl> pimpl_;
};
```

While the interface is mostly self-explanatory, the arguments to both the constructor and the execute() function are worth explaining. To meet the requirements, let’s discuss why using references to base class C++ I/O streams is generally a good design practice. First, the desire to use different I/O modes is quite common. Specifically, redirection to or from files is a frequently requested modification to a CLI. In fact, you’ll see this request in Chapter 8! Second, implementing the generic versus specific interface adds virtually no complexity. For example, instead of directly writing to cout, one simply keeps a reference to an output stream and writes to that instead. In the base case, this reference simply points to cout. Finally, using arbitrary stream input and output greatly simplifies testing. While the program may instantiate the Cli class using cin and cout, tests can instantiate the Cli class with either a file stream or a string stream. In this manner, interactive stream inputs and outputs can be simulated using strings or files. This strategy simplifies testing of the Cli class since inputs can be easily passed in and outputs easily captured as strings rather than through standard input and output.

### 5.2.2.2 The Implementation

The implementation of the Cli class is worth examining to observe the simplicity enabled by the modularity of pdCalc’s design. The entire implementation of the Cli class is effectively contained in the execute() and postMessage() member functions. The execute() function drives the CLI. It presents a startup message to the end user, waits for commands to be entered, tokenizes these commands, and raises events to signal to the command dispatcher that a new command has been entered. The stackChanged() function is an observer proxy callback target that writes the top of the stack to the command line after the stackChanged() event is raised. Essentially, the CLI reduces to two I/O routines where execute() handles input and stackChanged() handles output. Let’s look at the implementations for these two functions starting with the execute() function shown in Listing 5-5.

**Listing 5-5. The execute() Function**

```
void Cli::CliImpl::execute(bool suppressStartupMessage, bool echo)
{
    if (!suppressStartupMessage)
        startupMessage();

    for (string line; getline(in_, line, '\n');) {
        Tokenizer tokenizer{line};
        for (const auto& i : tokenizer) {
            if (echo) out_ << i << endl;
            if (i == "exit" || i == "quit")
                return;
            else
                parent_.raise(CommandEntered, make_shared<CommandData>(i));
        }
    }
    return;
}
```

The main algorithm for the CLI is fairly simple. First, the CLI waits for the user to input a line. Second, this input line is tokenized by the Tokenizer class. The CLI then loops over each token in the input line and raises an event with the token string as the event’s data. The CLI terminates when it encounters either a quit or an exit token.

The only piece of the execute() function not previously explained is the Tokenizer class. Simply, the Tokenizer class is responsible for taking a string of text and splitting this string into individual space-separated tokens. Neither the CLI nor the Tokenizer determines the validity of tokens. Tokens are simply raised as events for the command dispatcher to process. Note that as an alternative to writing your own, many libraries (boost, for example) provide simple tokenizers.

Given the simplicity of the tokenization algorithm (see the implementation in Tokenizer.cpp), why did I design the Tokenizer as a class instead of as a function returning a vector of strings? Realistically, both designs functionally work, and both designs are equally easy to test and maintain. However, I prefer the class design because it provides a distinct type for the Tokenizer. Let’s examine the advantages of creating a distinct type for tokenization.

Suppose we wanted to tokenize input in function foo() but process tokens in a separate function, bar(). Consider the following two possible pairs of functions to achieve this goal:

```
// use a Tokenizer class
Tokenizer foo(const string&);
void bar(const Tokenizer&);
```

```
// use a vector of strings
vector<string> foo(const string&);
void bar(const vector<string>&);
```

First, using a Tokenizer class, the signatures for both foo() and bar() immediately inform the programmer the intent of the functions. We know these functions involve tokenization. Using a vector of strings leaves ambiguity without further documentation (I intentionally did not provide names for the arguments). More importantly, however, typing the tokenizer enables the compiler to ensure that bar() can only be called with a Tokenizer class as an argument, thus preventing a programmer from accidentally calling bar() with an unrelated collection of strings. Another benefit of the class design is that
