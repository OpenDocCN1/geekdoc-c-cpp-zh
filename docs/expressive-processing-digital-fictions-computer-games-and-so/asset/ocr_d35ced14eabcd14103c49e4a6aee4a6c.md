+   5. For the third mode, Meehan worked particularly on versions of Aesop's fables such as “The Fox and the Crow” and “The Ant and the Dove.”

+   6. This example and the one above are adapted from Meehan’s dissertation (1976, 195–196)—substituting other characters with those in this story.

+   7. This summary draws on Schank’s *Conceptual Information Processing* (1975a, 41–44).

+   8. Meehan calls them *delta-acts* in his dissertation, while Abelson and Schank call them *delicts* in their 1975 publications (Schank 1975b; Abelson 1975). I will alternate, depending on whose work I am referencing.

+   9. According to Meehan’s dissertation (1976, 50). The description of this portion of chapter 11’s story (ibid., 170) elides this step.

+   10. Ryan particularly notes Lucia Vania, Umberto Eco, David Lewis, and Lubomír Doležel—followed by the 1980s books of Dorrit Cohn and Thomas Pavel. In the first chapter of *Fictional Worlds*, Pavel (1986) sketches a similar topic of Doležel’s and Eco’s contributions, while also noting the importance of Ryan’s early essays on the topic.

+   11. Or to put it another way, a fiction’s events and their portrayal.

+   12. One interesting element of the *Tale-Spin* source code—either not present at the time of Meehan’s dissertation or not reported in it—is a question asking the audience “HOW LIBERAL-MINDED ARE YOU?” (0–3) “when the main character’s problem is *Sigma-Sex* (Meehan 1980, line 255). The answer “0” results in *Tale-Spin* requiring that the character’s sex interests be limited to opposite-gender and, if human, same-species characters. Other numbers relax one or both of these requirements. Above this, a comment reads “HOW LIBERAL-MINDED IS J. BEAR?” (NOT READER)” (line 2548). The further questioning of the audience on this topic appears, in the version of the code that I have, to remain unimplemented.

+   13. It is worth noting, however, that the traversal function model is only one of the models found in *Cybertext*. As Markku Eskelinen pointed out during the blog-based peer review of this book, another model (Aarseth 1997, 103–105) is significantly closer to the one I presented in this book’s introduction. Yet this model of Aarseth’s is only employed, within *Cybertext*, for the discussion of “adventure games”—and as far as I know it has not been adopted by any other critics.

+   14. Rather, Mumblle is composed primarily of rules that assemble texts. So, for example, rather than having different sentence templates to describe the location of different types of characters and objects, into which it inserts the name of the noun being described, we see code like this:

```
EXPR C'LOC' ();
BEGIN
IF ISVALPART = 00 OR ISVAL = 00
THEN IS RPLACA 'WHERE:
IF NULL ("SAID OF 'ACTOR) AND ISVALPART EQ 'HOME OF 'ACTOR
```