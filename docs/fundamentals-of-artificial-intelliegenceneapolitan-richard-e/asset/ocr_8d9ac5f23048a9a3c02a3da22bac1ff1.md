![](bbox=[0.13, 0.08, 0.95, 0.33])

Figure 15.3 Two parse trees for the sentence “right help left”.

success is true. However, it is switched to false if it is the top-level call and there are more words left to be parsed.

The value of function Parse is true if a successful parse is obtained and false otherwise. The function does not produce a parse tree. However, it can be readily modified to produce such a tree as follows. When a successful parse of a symbol is obtained, the function returns a pointer to a node containing that symbol. The symbol is then made a child of the symbol at the previous level. The pointer returned in the top-level call points to the root of the tree. It is left as an exercise to write this modification.

# 15.1.2 Ambiguity

Consider the following sentence, which might appear as a headline in the newspaper:

right help left.

This sentence could mean that the political right helped the political left, or it could mean the correct hired workers (the right help) left the premises. The difficulty is that the word “right” is both a noun and an adjective, the word “help” is both a verb and a noun, and the word “left” is both a noun and a verb. Using the grammar in Table 15.1, we can parse the sentence in two different ways shown in Figure 15.3. When a sentence can be parsed in more than one way, we say the sentence has syntactic ambiguity. There are many, more amusing forms of syntactic ambiguity, but many of them require a more complex grammar that allows preposition phrases. Table 15.2 shows such a grammar without the lexicon. Words that are Prepositions are words such as “by”, “of”, and “to”.