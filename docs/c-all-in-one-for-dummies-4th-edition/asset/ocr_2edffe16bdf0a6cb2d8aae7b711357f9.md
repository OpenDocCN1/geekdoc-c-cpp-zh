using functions. All this code goes inside curly brackets and is preceded by a class header. The header gives the name of the class. And, oh, yes, the word *public* is stuck in there, and it has a colon after it. The “Accessing members,” section later in this chapter explains the word `public`. By itself, this code isn’t very useful, but you put it to use in Listing 1-2, an application that you can actually compile and run.

# LISTING 1-1: Pen.h Contains the Class Description for Pen

```
```cpp
#ifndef PEN_H_INCLUDED
#define PEN_H_INCLUDED
using namespace std;
enum Color {
    blue,
    red,
    black,
    clear,
    grey
};

enum PenStyle {
    ballpoint,
    felt_tip,
    fountain_pen
};

class Pen {
public:
    Color InkColor;
    Color ShellColor;
    Color CapColor;
    PenStyle Style;
    float Length;
    string Brand;
    int InkLevelPercent;

    void write_on_paper(string words) {
        if (InkLevelPercent <= 0) {
            cout << "Oops! Out of ink!" << endl;
        }
        else {
            cout << words << endl;
```
```

*(continued)*