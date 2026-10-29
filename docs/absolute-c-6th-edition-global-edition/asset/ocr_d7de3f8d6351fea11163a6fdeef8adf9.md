of masculine pronouns with gender-neutral pronouns. For example, it will replace "he" with "she or he". Thus, the input sentence

```
See an adviser, talk to him, and listen to him.
```

should produce the following suggested changed version of the sentence:

```
See an adviser, talk to her or him, and listen to her or him.
```

Be sure to preserve uppercase letters for the first word of the sentence. The pronoun "his" can be replaced by "her(s)"; your program need not decide between "her" and "hers". Allow the user to repeat this for more sentences until the user says she or he is done. This will be a long program that requires a good deal of patience. Your program should not replace the string "he" when it occurs inside another word such as "here". A word is any string consisting of the letters of the alphabet and delimited at each end by a blank, the end of the line, or any other character that is not a letter. Allow your sentences to be up to 100 characters long.

# 6. There is a CD available for purchase that contains .jpeg and .gif images of music that is in the public domain. The CD includes a file consisting of lines containing the names, then composers of that title, one per line. The name of the piece is first, then zero or more spaces then a dash (-) character, then one or more spaces, then the composer’s name. The composer name may be only the last name, an initial and one name, two names (first and last), or three names (first, middle, and last). There are a few tunes with "no author listed" as author. In the subsequent processing, "no author listed" should not be rearranged. Here is a very abbreviated list of the titles and authors.

+   1. Adagio "MoonLight" Sonata - Ludwig Van Beethoven
+   2. An Alexis - F.H. Hummel and J.N. Hummel
+   3. A La Bien Aimee - Ben Schutt
+   4. At Sunset - E. MacDowell
+   5. Angelus - J. Massenet
+   6. Anitra's Dance - Edward Grieg
+   7. Ase's Death - Edward Grieg
+   8. Au Matin - Benj. - Godard
+   ...

+   37. The Dying Poet - L. Gottschalk
+   38. Dead March - G.F. Handel
+   39. Do They Think of Me At Home - Chas. W. Glover
+   40. The Dearest Spot - W.T. Wrighton

+   1. Evening - L. Van Beethoven
+   2. Embarrassment - Franz Abt
+   3. Erin is my Home - no author listed
+   4. Ellen Bayne - Stephen C. Foster
+   ...