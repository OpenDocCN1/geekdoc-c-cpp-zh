+   - Regular expressions are a syntax for string parsing that have a power roughly equal to regular grammagrams.  
+     - Character classes can represent a set of characters that can be matched. You can build character classes with square brackets. There are also a number of built-in character classes for common used sets of characters.  
+     - Quantifiers specify that a character of grouping can be present certain numbers of times. Quantifiers include ?, *, and +.  
+     - Strings can be turned into **Regex** using the **r** method. The **Regex** object has methods called **findAllIn** and **replaceAllIn**. They can also be used at patterns.

+   - Context-Free Parsers  
+     - The **combinator parser** library in Scala makes it easy to build a parser from a CF grammar.  
+     - Default output of parsers include a mix or strings, `~` objects, and lists. This can be challenging to work with.  
+     - Using the `~` operator you can force parsers to output specific types that you want.

# 30.5.2  Exercises

+   1. Write a simple program that will take a Chomsky grammar and allow the user to generate strings from the language.
+   
+   2. For each of the following grammars, try to figure out what languages they generate. For those that are regular, create an appropriate regular expression. For that that are context free, write appropriate parsing code.
+      - $\begin{aligned} S& \rightarrow A \\ A& \rightarrow a A \mid B \\ B& \rightarrow b B \mid b \end{aligned}$  
+      - $\begin{aligned} S& \rightarrow a A \\ A& \rightarrow a A \mid b C \\ C& \rightarrow c C \mid c \end{aligned}$  
+      - $\begin{aligned} S& \rightarrow A B C \\ A& \rightarrow a A \mid a \\ B& \rightarrow b B \mid b \\ c& \rightarrow c C \mid c \end{aligned}$  
+      - $\begin{aligned} S& \rightarrow A B \\ A& \rightarrow a A \mid a \\ B& \rightarrow A b B \mid b \end{aligned}$  
+      - $\begin{aligned} S& \rightarrow e L A e \\ e L A& \rightarrow e R A \end{aligned}$  
+      - $\begin{aligned} A L A& \rightarrow A A L \\ A R e& \rightarrow A L A e \\ A R A& \rightarrow R A A \end{aligned}$
+   
+   3. Try to come up with, or look up, a simple context-free grammar for English. Write a parser for it and include a simple dictionary.