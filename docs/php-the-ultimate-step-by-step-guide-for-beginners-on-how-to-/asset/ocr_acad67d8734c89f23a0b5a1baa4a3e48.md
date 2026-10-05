We're going to do an inquiry with a specific WHERE condition, and afterward utilize EXPLAIN to get insights about how it was prepared by MySQL:

SELECT * FROM creators WHERE creator = 'Arnold Robbins';

The EXPLAIN output gives an abundance of data about how MySQL prepared the question.

It tells you:

+   • That're utilizing the creators table.

+   • The question sort is ALL, every record is filtered to check for the right esteem.

+   • The possible_keys is NULL in light of the fact that no record matches.

+   • The key utilized by this question is as of now NULL.

+   • The key_len is the key length; as of now NULL, as no key was utilized.

+   • The ref section shows which segments or constants are utilized with the key; at present NULL.

+   • The quantity of columns that must be looked through.

Notice that a large number of the qualities have changed with respect to the indexing:

+   • ref implies that lines with coordinating list qualities are read from this table for matches.

+   • possible_keys shows a conceivable key of authind.

+   • key shows that the authind key was utilized.

+   • key_len shows the length of the key as 126.

+   • ref lets you know that a consistent key is being utilized.

+   • columns demonstrate that one line was sought, which is a great deal not some time recently.

The correlation demonstrates that adding the index spares a great deal of processing time even for little tables.

# Selecting with the LEFT JOIN ON Clause

We've talked about performing joins in our SELECT statements utilizing the WHERE provision, be that as it may, there's another approach to join tables.