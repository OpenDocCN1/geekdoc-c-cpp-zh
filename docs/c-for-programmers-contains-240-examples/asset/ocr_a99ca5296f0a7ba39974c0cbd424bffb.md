We have already discussed how the asterisk (*) and plus (+) quantifiers work. The question mark (?) quantifier matches zero or one occurrences of the pattern that it quantifies. A set of braces containing one number, {n}, matches exactly n occurrences of the pattern it quantifies. We demonstrate this quantifier in the next example. Including a comma after the number enclosed in braces matches at least n occurrences of the quantified pattern. The set of braces containing two numbers, {n,m}, matches between n and m occurrences (inclusively) of the pattern that it quantifies. All of the quantifiers are greedy—they will match as many occurrences of the pattern as possible until the pattern fails to make a match. If a quantifier is followed by a question mark (?), the quantifier becomes lazy and will match as few occurrences as possible as long as there is a successful match.

| Quantifier | Matches |
|---|---|
| * | Matches zero or more occurrences of the preceding pattern. |
| + | Matches one or more occurrences of the preceding pattern. |
| ? | Matches zero or one occurrences of the preceding pattern. |
| {n} | Matches exactly n occurrences of the preceding pattern. |
| {n,} | Matches at least n occurrences of the preceding pattern. |
| {n,m} | Matches between n and m (inclusive) occurrences of the preceding pattern. |

Fig. 21.3 | Quantifiers used in regular expressions.

# 21.7.2 Validating User Input with Regular Expressions

The program in Fig. 21.4 presents a more involved example that uses regular expressions to validate name, address and telephone number information input by a user.

```
1  // Fig. 21.4: Validate.cpp
2  // Validating user input with regular expressions.
3  #include <iostream>
4  using std::cin;
5  using std::cout;
6  using std::endl;
7
8  #include <string>
9  using std::string;
10
11 #include "boost/regex.hpp"
12
13 bool validate( const string&, const string& ); // validate prototype
14 string inputData( const string&, const string& ); // inputData prototype
15
16 int main()
17 {
18     // enter the last name
19     string lastName = inputData( "last name", "[A-Z][a-zA-Z]*" );
```

Fig. 21.4 | Validating user input with regular expressions. (Part 1 of 3.)