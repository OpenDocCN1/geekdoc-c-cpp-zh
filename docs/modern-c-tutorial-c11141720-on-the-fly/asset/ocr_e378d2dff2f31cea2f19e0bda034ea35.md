# 6.2 std::regex and Its Related

Character Description

+   + matches the previous subexpression one or more times. For example, foo+ matches foo
and fooo but does not match fo. + is equivalent to {1}.
? matches the previous subexpression zero or one time. For example, Your(s)? can match
Your in or Yours. ? is equivalent to {0,1}.
{n} is a non-negative integer. Matches the n times. For example, o{2} cannot
match o in for, but can match two o in foo.
{n,} is a non-negative integer. Matches at least n times. For example, o{2} cannot match o
in for, but matches all o in foooooo. o{1} is equivalent to o+. o{0} is equivalent to
*:
{n,m} m and n are non-negative integers, n is less or equal to m. For, o{1,3} will match the first three o in
fooooo. o(0,1) is equivalent to?. Note that there are no spaces between the
comma and the two numbers.

With these tables, we can read almost all regular expressions.

# 6.2 std::regex and Its Related

The most common way to match string content is to use regular expressions. Unfortunately, in
traditional C++, expressions have not been supported by the language level, and are not included
in the standard library. C++ is a high-performance language. In the development of backend services,
t use of regular expressions is also used when joining URL links. The most mature and
common practice in today.

The general solution is to use the regular expression library of boost. C++11 officially incorporates
t processing of regular expressions into the standard library, providing standard support from the
language level and no longer relying on third parties.

The regular expression provided by C++11 operates on the std::regex object, and the
pattern std::regex (essentially std::basic_regex) is initialized and matched by std::regex_match
Produces std::match (essentially the std::match_results object).

We use a example to briefly introduce this use library. Consider the following regular
expression:

+   [az].txt: In this expression, [az] means matching a lowercase letter, + can match the
previous expression multiple times, so [az]+ matches a string of lowercase letters. In the
regular expression, a means to match any character, and \ means to match the character ,
and the last txt means to match exactly three letters. So the content of this regular expression
to is a test file containing pure lowercase letters.

std::regex_match is used to match strings and regular expressions, and there are many different