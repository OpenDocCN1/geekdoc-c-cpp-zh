
> 14. By this I do not mean to argue that statistical AI is particularly fallible within the world of AI. In fact, the rise of statistical AI is precisely due to its greater successes. What I mean to argue against here is the belief that AI...
> 
> Notes continued at end of this chapter.

recommendation system. At the same time, statistical techniques have severe limitations, which are not always acknowledged.

## Limits of Statistical AI

In the United States, our most substantial public conversation about the limits of statistical AI arose in response to the Total Information Awareness (TIA) initiative. Though often discussed as a response to the terrorist attacks of September 11, 2001, the TIA effort was first proposed by the Defense Advanced Research Projects Agency two years before—and it was the continuation of a vision with a significantly longer history. But it was not until after the 2001 attacks that TIA gained serious momentum of its own, after acquiring major funding and a high-profile director—John Poindexter, best known for less-than-truthful testimony to Congress about the Iran-Contra scandal that plagued President Ronald Reagan’s administration.

The TIA vision is an example of dystopian magical thinking. It is dystopian in that, rather than identifying potential criminals and placing them under surveillance, it imagines putting every citizen under surveillance. It is magical thinking in that it imagines statistical AI techniques are capable of sifting through the vast flood of information this would produce in order to identify good leads for antiterrorism investigators.14 This demonstrates a fundamental misunderstanding of how these techniques operate. One of the world’s most respected computing organizations—the Association for Computing Machinery—put it this way in a letter to the Senate Armed Services Committee:

Any type of statistical analysis inevitably results in some number of false positives—in this case incorrectly labeling someone as a potential terrorist. As the entire population would be subjected to TIA surveillance, even a small percentage of false positives would result in a large number of law-abiding Americans being mistakenly labeled.

For example, suppose the system has a 99.9% accuracy rate. We believe that having only 0.1% of records being misclassified as belonging to potential terrorists would be an unachievable goal in practice. However, if records for everyone in the U.S. were processed monthly, even this unlikely low rate of false positives could result in as many as 3 million citizens being wrongly identified each year. More realistic assumptions about the percentage of false positives would drive the number even higher. (Simons and Spafford 2003)

False positives are fine in Google link lists and Amazon purchase recommendations, but in other areas their cost is much too high. In the area of surveillance, not only would they improperly cast suspicion on many people; the number of false leads would also be so high as to overwhelm any group tasked with investigating them. Further, the problem of false positives is only one of the serious limitations of statistical techniques. Another is the need for large amounts of well-defined data in order to develop the system’s model. The amount of information available on terrorist activity is small by comparison with that used to build effective statistical systems (e.g., Google’s collection of web pages containing links—and the patterns sought (e.g., determining whether a conversation is somehow “suspicious”) are extremely ill defined compared with statistical AI’s success stories (e.g., determining where a web page links). As security expert Bruce Schneier

(2006) estimates, an “unrealistically accurate” TIA system would generate one billion false alarms for every real plot identified. Further, there is the problem of false negatives. Even with all these billions of alarms, the system would fail to go off at times it should.

In 2003, after public outcry, Poindexter resigned, and it seemed that TIA had been dealt a deathblow when its funding was removed. Then, in 2005, the New York Times reported that the Bush administration had authorized a far-reaching National Security Agency surveillance program that included warrantless electronic eavesdropping on telephone calls and emails of U.S. citizens, and a series of further revelations followed (Williams 2006). If not TIA in name, this was clearly the same dystopian vision at work. Other manifestations of magical thinking also continue to generate proposals for utterly inappropriate attempts to employ statistical techniques. In the case of surveillance, even if ineffective for their stated purpose, these efforts still produce databases and monitoring systems, each vulnerable to compromise and improper use.

More generally, to understand what statistical techniques can accomplish, we need to move beyond general principles. Though understanding the basic fact of false positives provides some basis for evaluating proposals for statistical techniques (the cost of false positives must be low), it is also important to foster an understanding of how statistical models are developed and what they represent. As I argued in the introduction—and will expand on in this chapter’s conclusion—I believe presenting legible examples, especially from the area of media authoring, can help in this effort. And of course,

such examples can also help one consider when statistical techniques might be useful to media authors.

## N-grams

A statistical model used in a system for understanding or generating human language is often called a “language model.” As with most statistical models, the primary use of a language model is to predict the future (linguistic) behavior of a system based on a sample of its past (linguistic) behavior. Constructing such a model requires two efforts. The first is deciding what to pay attention to: what “features” of the past behavior will be treated statistically. The second is deciding how to make those features part of an operating statistical model.

One of the most popular approaches for building a language model is the concept of n-grams (also known as Markov chains). An n-gram language model is built by looking at a body of language data and seeing what elements follow other elements. If looking at the letters in a body of English, q would quite often be followed by u. Looking at the word level, you would more frequently be followed by are than by banana. Looking at sets of two elements is examining bigrams and sets of three are trigrams.

As this probably makes clear, in an n-gram model, the features are often the word or two that appear before the current one. A simple model employing these features would be: the different following words are assigned likelihoods based on how frequently they appear after the preceding ones within the sample data. In actuality, the models tend to be somewhat more complicated. This is in part because even after training on millions of words, new pairs and triplets of words will appear regularly even in

data from the same source (say, the same newspaper from which the model was developed). This requires that the model be “smoothed” so that newly appearing bigrams and trigrams won’t be assigned zero probabilities.

Such models have many potential uses. For example, dictation software may find certain words in a sentence ambiguous. But an n-gram model can use the words that precede and follow ambiguous words to improve the chances of correct recognition. Certainly “ate the banana” is a much more likely trigram than “ate the bandana.”

On the other hand, an n-gram collection doesn’t “understand” anything about the language it models. It would work just the same way on a collection of musical notes or any other serially ordered data. And while as a model it does well at capturing coherence from word to word, it does poorly at capturing any higher-level structure. This becomes quite apparent in the various attempts to use n-grams to generate language, rather than simply understand it. The foundational example here is Claude Shannon’s n-gram-generated sentence from his field-defining essay “A Mathematical Theory of Communication”:

> THE HEAD AND IN FRONTAL ATTACK ON AN ENGLISH WRITER THAT THE CHARACTER OF THIS POINT IS THEREFORE ANOTHER METHOD FOR THE LETTERS THAT THE TIME OF WHO EVER TOLD THE PROBLEM FOR AN UNEXPECTED. (1948, 388)

This passage is more coherent than a random series of words, because each word follows quite naturally from the one preceding it. This is no surprise, given that it was produced by flipping through a book, writing down a word, flipping through until that word was found again,
