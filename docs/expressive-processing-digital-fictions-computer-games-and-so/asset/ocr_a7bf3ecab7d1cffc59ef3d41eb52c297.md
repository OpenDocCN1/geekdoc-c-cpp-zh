```
frame ivy is a object

default positive_iconic_features
is {leaves, vines} and

default negative_iconic_features is {poison} and

default negative_literary_modifiers
is {poisoness, tangled} and

default positive_literary_modifiers
is {spreading, green, lush},

(184)
```

This still is not enough to ensure the creation of sentences such as those seen from INDPSDs. The grammar needs to be further augmented with more consistency of structure and more direction about how to fill out aspects of the grammar. For this purpose Brutus contains what its authors call “literary constraints.” Here is the second version of the INDPSD, incorporating a set of such constraints:

+   • INDPSD → SETTING verb (isa possessive_verb) FP(n=3)
+   • FP → ‘its’ FEATURE FP | ‘its’ FEATURE
+   • SETTING → noun_phrase (has_role setting)
+   • FEATURE → noun_phrase (isa iconic_feature_of SETTING)

(185)

In the grammar above, the literary constraints are the elements that appear in parenthesis. For example, the “(n=3)” in the first line enforces the occurrence of three FPs in the sentence—creating the three-part parallelism seen in examples of the INDPSD. This is simply a