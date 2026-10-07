```
ostream & nifty:operator<<(ostream & nifty & n)
{
  os << n;
}
```

5. Consider the following class declaration:

```
class Golfer{
private:
  char * fullname;      // points to string containing golfer's name
  int games;             // holds number of golf games played
  int * scores;         // points to first element of array of golf scores
public:
  Golfer();
  Golfer(const char * name, int g= 0);
  // creates dynamic array of g elements if g > 0
  Golfer(const Golfer & g);
  -Golfer();
```

a. What methods could be invoked by each of the following statements?

```
Golfer nancy;               // #1
Golfer lulu("Little Lulu");  // #2
Golfer roy("Roy Hobbes", 12); // #3
Golfer * par = new Golfer;     // #4
Golfer next = lulu;             // #5
Golfer hazard = "Weed Thwacker"; // #6
*par = nancy;                // #7
nancy = "Nancy Putter";        // #8
```

b. The class requires several methods to make it useful. What additional method does it require to protect against data corruption?

# Programming Exercises

1. Consider the following class declaration:

```
class Cow {
  char name[20];
  char * hobby;
  double weight;
public:
  Cow();
  Cow(const char * nm, const char * ho, double wt);
  Cow(const Cow c4);
```