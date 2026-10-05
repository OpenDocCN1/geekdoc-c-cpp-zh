| Abbreviation | Stands For | Abbreviation | Stands For |
|---|---|---|---|
| \d | [[:digit:]] | \D | ^[:digit:]] |
| \s | [[:space:]] | \S | ^[:space:]] |
| \w | [[:alnum:]] | \W | ^[:alnum:]] |

**Table 28.2** Abbreviations for character classes.

To support international texts, there are specially designated group names. There are **collation groups (collations)** like [[[:span-ll:]]]. This allows ll to be matched as a single character in Spanish. With **equivalence groups** like [[=e]], an e and all its accented variants, è, é, and ê, can be matched in French.

#  28.2.10 Notes on Regular Expressions in C++ Expressions in Algorithm

For most applications, the subtleties of regular expression searching are probably irrelevant. Will a short string be found first, or one further up? Those who are more used to Perl or POSIX expressions might be confused, so we want to point out the small difference here.

Comparing the results of a search according to the POSIX standard and the ECMAScript standard yields the results shown in Table 28.3.