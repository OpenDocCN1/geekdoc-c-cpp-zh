# Literary Augmented Grammars

Just as Brutus uses story grammars, it also uses paragraph and sentence grammars. These are relatively standard linguistic tools, but in Brutus they are augmented with handcrafted literary knowledge and named LAGs. One particular LAG is the “independent parallel setting description” (INDPSD), which created this familiar sentence: “He loves the studious youth, ivy-covered clocktowers and its sturdy brick.” These are an example of using hand-authored data to generate sentences with literary nuance—making for better text as well as for more ability to reflect the underlying system in surface language. A closer look at the INDPSD reveals the strategies employed.

Bringsjord and Ferrucci present the INDPSD grammar three times in the course of explaining the version used in the “setting_description” from the story of Dave Striver. The first presentation is of a relatively standard, if somewhat specialized, grammar of:

+   - INDPSD -> SETTING verb FP
+   - FP -> 'its' FEATURE FP | 'its' FEATURE
+   - SETTING -> noun_phrase
+   - FEATURE -> noun_phrase

(2000, 181)

In this grammar, uppercase words are nonterminals, words in single quotes are literals (used in the sentence exactly as they appear), and lowercase words are terminals (to be selected/constructed from the lexicon). The “|” symbol, which did not appear in the story grammar, can be read as “or.” In this case, it indicates that an INDPSD