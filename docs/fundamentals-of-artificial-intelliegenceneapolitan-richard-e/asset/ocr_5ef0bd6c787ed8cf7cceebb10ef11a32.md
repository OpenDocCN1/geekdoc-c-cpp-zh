# 15.1.4 Probabilistic Parser

If we write the CYK algorithm as suggested at the end of the last section, we can retrieve all possible parse trees for a given sentence. However, our goal is ordinarily to retrieve the most likely parse tree or the several most likely parse trees. This matter is addressed by using a probabilistic context-free grammar (PCFG). Table 15.4 shows a PCFG.

Each rule in a PCFG has a probability associated with it. The probabilities for the rules for the a given category sum to 1. For example, there are three rules for Sentence, namely Rules 1, 2, and 3. We have that

P(Rule 1) + P(Rule 2) + P(Rule 3) = .6 + .25 + .15 = 1.

This means, for example, that if a string is a Sentence, then it has a .6 probability of being a NounPhrase followed by a VerbPhrase. For a category that is substituted by a terminal, we have written the set of all substitutions as one rule. So it is the probabilities in this one rule that sum to 1. For example, in Rule 12,

P(a) + P(an) + p(the) = .4 + .2 + .4 = 1.

This means, for example, that given that the word is an Article, it has a .4 probability of being an “a”. Of course, we have used a very small lexicon for the sake of example. In an actual application there would be many more words (perhaps approaching the entire dictionary), and each word would have a much smaller probability.

Figure 15.7 shows the parse trees in Figure 15.3 with probabilities from Table 15.4 added. We make independence assumptions similar to those in a Bayesian network. Namely, we assume, for example, that the P(right|Noun) = .15 regardless of the values of other nodes in the parse tree. Call the parse tree in Figure 15.7 (a) Parse_a and the one in Figure 15.7 (a) Parse_b. Given our assumptions, we have the following:

P(Parse_a) = .15 x .3 x .2 x .15 x .3 x .8 x .65 = 2.11 x 10^-4

P(Parse_b) = .2 x .1 x .3 x .1 x .2 x .65 = 7.8 x 10^-5.

So we choose Parse_a because it is more probable. Because these are the only two parses of the sentence “right help left”, the probability of the sentence is 2.11 x 10^-4 + 7.8 x 10^-5 = 2.89 x 10^-4.

To find the most probable parse from the array of pointers produced by the CYK algorithm, we can simply find all the parse trees and choose the most probable one. However, if we only want the most probable one (or few most probable ones), we can search the space of all parse trees using a best-first search algorithm called A* [Dechter and Pearl, 1985].

The parse with the highest probability is not necessarily the sensible one.

Consider again this sentence.

I shot an elephant in my pajamas.