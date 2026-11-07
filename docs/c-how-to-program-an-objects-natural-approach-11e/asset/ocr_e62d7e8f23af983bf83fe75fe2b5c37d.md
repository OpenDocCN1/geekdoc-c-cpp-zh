+   - **Stemming**—reducing words to their stems by removing prefixes or suffixes. For example, the stem of “varieties” is “varieti.”
+   - **Lemmatization**—like stemming, but produces real words based on the original words’ context. For example, the lemmatized form of “varieties” is “variety.”
+   - **Word frequency counting**—determining how often each word appears in a corpus.
+   - **Stop-word elimination**—removing common words, such as *a*, *an*, *the*, *I*, *we*, *you* and more, to analyze the important words in a corpus.
+   - **n-grams**—producing sets of consecutive words in a corpus to identify words frequently appearing adjacent to one another. n-grams are commonly used for predictive text input, such as when your smartphone suggests possible next words as you type a text message.

This case study exercise serves two purposes:

+   - First, it introduces the crucial AI subtopic of natural language processing, which will play a key role in the future of anyone learning programming today.
+   - Second, it introduces the NLP subtopic of similarity detection, which you’ll perform using straightforward array-, string- and file-processing techniques.

# ### Project Gutenberg

A great source of text for analysis is Project Gutenberg’s massive collection of free e-books:

https://www.gutenberg.org

The site contains over 70,000 e-books in various formats, including plain-text files. These are out of copyright in the United States. For information about Project Gutenberg’s Terms of Use and copyright in other countries, see:

https://gutenberg.org/policy/terms_of_use.html

For this case-study exercise, you’ll use the plain-text e-book files for William Shakespeare’s *Romeo and Juliet*:

https://gutenberg.org/ebooks/1513

and Christopher Marlowe’s *Edward the Second*:

https://gutenberg.org/ebooks/20288

Each of these is available free for download at Project Gutenberg.

# ### Downloading E-Books from Project Gutenberg

Project Gutenberg does not allow programmatic access to its e-books. You must download the books to your own system before analyzing them.<sup>35</sup> To download *Romeo and Juliet* as a plain-text file, right-click the Plain Text UTF-8 link on the play’s web page, then select

+   - Save Link As... (Chrome/Firefox/Microsoft Edge),
+   - Download Linked File As... (Safari), or