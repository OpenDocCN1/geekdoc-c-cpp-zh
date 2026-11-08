Second: You could come up with a reasonable behavior for such corner cases. Come up with some result the function could compute for empty input. Say, a not-a-number value for the `largest()` of an empty array?

Both can at times be viable options. But can you, in the spirit of this chapter, work out a third alternative?

Exercise 9-5. As promised, write yet another variant of `Ex8_09A`, `Ex8_09B`, and `Ex8_09C`, where this time the `average10()` function uses one of the vocabulary types seen in this chapter. Show that this one function can be called both for fixed-size C-style arrays and `std::array<>` containers, and only so for arrays of ten elements.

Exercise 9-6. Suppose you have a `vector<>` and you know for a fact that it contains exactly ten elements (or at least ten elements). Can you then call the `average10()` function of the previous example to compute the average of these ten elements (or the ten first elements)? Not directly, obviously, but it is possible! After all, all the necessary `data` (ten consecutive elements) is present in the vector. You may want to consult a Standard Library reference for this.