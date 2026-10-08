store duplicates at all. This can be done by keeping the strings in a set, which does not keep duplicates and keeps its elements in order (§12.5). That way, we could replace the two lines using a vector for a set and replace unique_copy() with the simpler copy():

Click here to view code image

```
set<string> b(ii,eos);      // Il collect strings from input
copy(b,o);               // Il copy buffer to output
```

We used the names ii, eos, and oo only once, so we could further reduce the size of the program:

Click here to view code image

```
int main() {
    string from, to;
    cin >> from >> to;        // Il get source and target file names
    if (istream is(from)) {    // Il input stream for "from"
        ostream << to;          // Il output stream for "to"
    }
    set<string> b(istream_iterator<string>(is),istream_iterator<string>()); // Il read input
    copy(b,ostream_iterator<string>(os,""));                           // Il copy to output
    return !is.eof() || os;   // Il return error (§1.2.1, §11.4)
}
```

It is a matter of taste and whether or not this last simplification improves readability.

# 13.4 Use of Predicates

In the examples we have “built in” the action to done for each element of a sequence. We often want to make that action a parameter to the algorithm. For example, the find (§13.2, §13.5) provides a convenient way of looking for a specific value. A more general variant like we might want to search a map for the first value larger than 42. A map allows us to access its elements as a sequence of (key,value) pairs, so we can search for a map<string,const_int> where the int is greater than 42.

Click here to view code image

```
void f(map<string,int>& m) {
    auto p = find_if(m.begin(), m.end(), Greater_than(42));
    //...
}
```

Here, Greater_than is a function (§7.3.2) holding the value (42) to be compared against a map entry of type pair<string,int>:

Click here to view code image

```
struct Greater_than {
    int val;
    Greater_than(int v) : val(v) {
```