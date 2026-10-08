
## 10.6 I/O error handling

This data file contains a sequence of (hour,temperature) pairs. The hours are numbered 0 to 23 and the temperatures are in Fahrenheit. No further formatting is assumed; that is, the file does not contain any special header information (such as where the reading was taken), units for the values, punctuation (such as parentheses around each pair of values), or termination indicator. This is the simplest case.

We could represent a temperature reading by a Reading type:

```cpp
struct Reading { // a temperature reading
    int hour; // hour after midnight [0:23]
    double temperature; // in Fahrenheit
};
```

Given that, we could read like this:

```cpp
vector<Reading> temps; // store the readings here
int hour;
double temperature;
while (ist >> hour >> temperature) {
    if (hour < 0 || 23 < hour) error("hour out of range");
    temps.push_back(Reading{hour,temperature});
}
```

This is a typical input loop. The istream called ist could be an input file stream (ifstream) as shown in the previous section, an (alias for) the standard input stream (cin), or any other kind of istream. For code like this, it doesn’t matter exactly from where the istream gets its data. All that our program cares about is that ist is an istream and that the data has the expected format. The next section addresses the interesting question of how to detect errors in the input data and what we can do after detecting a format error.

Writing to a file is usually simpler than reading from one. Again, once a stream is initialized we don’t have to know exactly what kind of stream it is. In particular, we can use the output file stream (ofstream) from the section above just like any other ostream. For example, we might want to output the readings with each pair of values in parentheses:

```cpp
for (int i=0; i<temps.size(); ++i)
    ost << '(' << temps[i].hour << ',' << temps[i].temperature << ')\n';
```

The resulting program would then be reading the original temperature reading file and producing a new file with the data in (hour, temperature) format. Because the file streams automatically close their files when they go out of scope, the complete program becomes

```cpp
#include "std_lib_facilities.h"

struct Reading {      // a temperature reading
    int hour;         // hour after midnight [0:23]
    double temperature; // in Fahrenheit
};

int main()
{
    cout << "Please enter input file name: ";
    string iname;
    cin >> iname;
    ifstream ist {iname};     // ist reads from the file named iname
    if (!ist) error("can't open input file ", iname);

    string oname;
    cout << "Please enter name of output file: ";
    cin >> oname;
    ofstream ost {oname};     // ost writes to a file named oname
    if (!ost) error("can't open output file ", oname);

    vector<Reading> temps;     // store the readings here
    int hour;
    double temperature;
    while (ist >> hour >> temperature) {
        if (hour < 0 || 23 < hour) error("hour out of range");
        temps.push_back(Reading{hour, temperature});
    }

    for (int i=0; i<temps.size(); ++i)
        ost << '(' << temps[i].hour << ','
            << temps[i].temperature << ')\n';
}
```

When dealing with input we must expect errors and deal with them. What kind of errors? And how? Errors occur because humans make mistakes (misunderstanding instructions, mistyping, letting the cat walk on the keyboard, etc.), because files fail to meet specifications, because we (as programmers) have the wrong expectations, etc. The possibilities for input errors are limitless! However, an `istream` reduces all to four possible cases, called the *stream state*:

| Stream states | Description |
| :--- | :--- |
| `good()` | The operations succeeded. |
| `eof()` | We hit end of input (“end of file”). |
| `fail()` | Something unexpected happened (e.g., we looked for a digit and found 'x'). |
| `bad()` | Something unexpected and serious happened (e.g., a disk read error). |

Unfortunately, the distinction between `fail()` and `bad()` is not precisely defined and subject to varying opinions among programmers defining I/O operations for new types. However, the basic idea is simple: If an input operation encounters a simple format error, it lets the stream `fail()`, assuming that you (the user of our input operation) might be able to recover. If, on the other hand, something really nasty, such as a bad disk read, happens, the input operation lets the stream go `bad()`, assuming that there is nothing much you can do except to abandon the attempt to get data from that stream. A stream that is `bad()` is also `fail()`. This leaves us with this general logic:

```cpp
int i = 0;
cin >> i;
if (!cin) {  // we get here (only) if an input operation failed
    if (cin.bad()) error("cin is bad");  // stream corrupted: let's get out of here!
    if (cin.eof()) {
        // no more input
        // this is often how we want a sequence of input operations to end
    }
    if (cin.fail()) {   // stream encountered something unexpected
        cin.clear();    // make ready for more input
        // somehow recover
    }
}
```

The `!cin` can be read as “cin is not good” or “Something went wrong with cin” or “The state of cin is not good().” It is the opposite of “The operation succeeded.” Note the `cin.clear()` where we handle `fail()`. When a stream has failed, we might be able to recover. To try to recover, we explicitly take the stream out of the `fail()` state, so that we can look at characters from it again; `clear()` does that – after `cin.clear()` the state of `cin` is `good()`.

Here is an example of how we might use the stream state. Consider how to read a sequence of integers that may be terminated by the character `*` or an “end of file” (Ctrl+Z on Windows, Ctrl+D on Unix) into a **vector**. For example:

1 2 3 4 5 *

This could be done using a function like this:

```cpp
void fill_vector(istream& ist, vector<int>& v, char terminator)
{
    // read integers from ist into v until we reach eof() or terminator
    
    for (int i; ist >> i;) v.push_back(i);
    if (ist.eof()) return;    // fine: we found the end of file
    
    if (ist.bad()) error("ist is bad");    // stream corrupted; let's get out of here!
    if (ist.fail()) {    // clean up the mess as best we can and report the problem
        ist.clear();    // clear stream state,
                         // so that we can look for terminator
        
        char c;
        ist >> c;    // read a character, hopefully terminator
        if (c != terminator) {    // unexpected character
            ist.unget();    // put that character back
            ist.clear(ios_base::failbit);    // set the state to fail()
        }
    }
}
```

Note that when we didn't find the terminator, we still returned. After all, we may have collected some data and the caller of `fill_vector()` may be able to recover from a `fail()`. Since we cleared the state to be able to examine the character, we have to set the stream state back to `fail()`. We do that with `ist.clear(ios_base::failbit)`. Note this potentially confusing use of `clear()`: `clear()` with an argument actually sets the `iostream` state flags (bits) mentioned and (only) clears flags not mentioned. By setting the state to `fail()`, we indicate that we encountered a format error, rather than something more serious. We put the character back into `ist` using `unget()`, the caller of `fill_vector()` might have a use for it. The `unget()` function is a shorter version of `putback()` (§6.8.2, §B.7.3) that relies on the stream remembering which character it last produced, so that you don't have to mention it.

If you called `fill_vector()` and want to know what terminated the read, you can test for `fail()` and `eof()`. You could also catch the `runtime_error` exception thrown by `error()`, but it is understood that getting more data from `istream` in the `bad()` state is unlikely. Most callers won't bother. This implies that in almost all
