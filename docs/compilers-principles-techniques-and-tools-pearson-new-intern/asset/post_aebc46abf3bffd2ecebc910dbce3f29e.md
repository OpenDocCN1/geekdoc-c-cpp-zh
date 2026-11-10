
## 5.5. IMPLEMENTING L-ATTRIBUTED SDD’s

![](img/a29d16e454785bb105e96ef448ac07f6_351_0.png)

Figure 5.35: Expansion of S with synthesized attribute constructed on the stack

which it must, or else we would not have expanded S in this way. After while and ( are popped off the stack, the code for the action-record is executed. It generates values for L₁ and L₂, and we take the shortcut of copying them directly to the inherited attributes that need them: S₁.next and C.true. The last two steps of the action cause L₁ and L₂ to be copied into the record called “Synthesize S₁.code.”

The synthesize-record for S₁ does double duty: not only will it hold the synthesized attribute S₁.code, but it will also serve as an action-record to complete the evaluation of the attributes for the entire production S → while ( C ) S₁. In particular, when it gets to the top, it will compute the synthesized attribute S.code and place its value in the synthesize-record for the head S.

When C becomes the top of the stack, it has both its inherited attributes computed. By the inductive hypothesis stated above, we suppose it correctly generates code to execute its condition and jump to the proper label. We also assume that the actions performed during the expansion of C correctly place this code in the record below, as the value of synthesized attribute C.code.

After C is popped, the synthesize-record for C.code becomes the top. Its code is needed in the synthesize-record for S₁.code, because that is where we concatenate all the code elements to form S.code. The synthesize-record for C.code therefore has an action to copy C.code into the synthesize-record for S₁.code. After doing so, the record for token ) reaches the top of stack, and causes a check for ) on the input. Assuming that test succeeds, the record for S₁ becomes the top of stack. By our inductive hypothesis, this nonterminal is expanded, and the net effect is that its code is correctly constructed and placed in the field for \(code\) in the synthesize-record for \(S_1\).

Now, all the data fields of the synthesize-record for S₁ have been filled in, so when it becomes the top of stack, the action in that record can be executed. The action causes the labels and code from C.code and S₁.code to be concatenated in the proper order. The resulting string is placed in the record below; that is, in the synthesize-record for S. We have now correctly computed S.code, and when the synthesize-record for S becomes the top, that code is available for placement in another record further down the stack, where it will eventually be assembled into a larger string of code implementing a program element of which this S is a part. □

### Can We Handle L-Attributed SDD’s on LR Grammars?

In Section 5.4.1, we saw that every S-attributed SDD on an LR grammar can be implemented during a bottom-up parse. From Section 5.5.3, every L-attributed SDD on an LL grammar can be parsed top-down. Since LL grammars are a proper subset of the LR grammars, and the S-attributed SDD’s are a proper subset of the L-attributed SDD’s, can we handle every LR grammar and L-attributed SDD bottom-up?

We cannot, as the following intuitive argument shows. Suppose we have a production \(A \to BC\) in an LR grammar, and there is an inherited attribute \(B.i\) that depends on inherited attributes of \(A\). When we reduce to \(B\), we still have not seen the input that \(C\) generates, so we cannot be sure that we have a body of production \(A \to BC\). Thus, we cannot compute \(B.i\) yet, since we are unsure whether to use the rule associated with this production.

Perhaps we could wait until we have reduced to \(C\), and know that we must reduce \(BC\) to \(A\). However, even then, we do not know the inherited attributes of \(A\), because even after reduction, we may not be sure of the production body that contains this \(A\). We could reason that this decision, too, should be deferred, and therefore further defer the computation of \(B.i\). If we keep reasoning this way, we soon realize that we cannot make any decisions until the entire input is parsed. Essentially, we have reached the strategy of “build the parse tree first and then perform the translation.”

### 5.5.4 Bottom-Up Parsing of L-Attributed SDD’s

We can do bottom-up every translation that we can do top-down. More precisely, given an L-attributed SDD on an LL grammar, we can adapt the grammar to compute the same SDD on the new grammar during an LR parse. The “trick” has three parts:

- 1. Start with the SDT constructed as in Section 5.4.5, which places embedded actions before each nonterminal to compute its inherited attributes and an action at the end of the production to compute synthesized attributes.
- 2. Introduce into the grammar a marker nonterminal in place of each embedded action. Each such place gets a distinct marker, and there is one production for any marker *M*, namely *M* → ε.
- 3. Modify the action *a* if marker nonterminal *M* replaces it in some production *A* → α {*a*} β, and associate with *M* → ε an action *a′* that
  - (a) Copies, as inherited attributes of *M*, any attributes of *A* or symbols of α that action *a* needs.
  - (b) Computes attributes in the same way as *a*, but makes those attributes be synthesized attributes of *M*.

This change appears illegal, since typically the action associated with production *M* → ε will have to access attributes belonging to grammar symbols that do not appear in this production. However, we shall implement the actions on the LR parsing stack, so the necessary attributes will always be available a known number of positions down the stack.

**Example 5.25:** Suppose that there is a production *A* → *B C* in an LL grammar, and the inherited attribute *B.i* is computed from inherited attribute *A.i* by some formula *B.i* = *f*(*A.i*). That is, the fragment of an SDT we care about is

*A* → {*B.i* = *f*(*A.i*); } *B C*

We introduce marker *M* with inherited attribute *M.i* and synthesized attribute *M.s*. The former will be a copy of *A.i* and the latter will be *B.i*. The SDT will be written

*A* → *M B C*
*M* → {*M.i* = *A.i*; *M.s* = *f*(*M.i*);}

Notice that the rule for *M* does not have *A.i* available to it, but in fact we shall arrange that every inherited attribute for a nonterminal such as *A* appears on the stack immediately below where the reduction to *A* will later take place. Thus, when we reduce ε to *M*, we shall find *A.i* immediately below it, from where it may be read. Also, the value of *M.s*, which is left on the stack along with *M*, is really *B.i* and properly is found right below where the reduction to *B* will later occur. □

**Example 5.26:** Let us turn the SDT of Fig. 5.28 into an SDT that can operate with an LR parse of the revised grammar. We introduce a marker *M* before *C* and a marker *N* before *S₁*, so the underlying grammar becomes

```
S → while ( M C ) N S₁
M → ε
N → ε
```

### Why Markers Work

Markers are nonterminals that derive only ε and that appear only once among all the bodies of all productions. We shall not give a formal proof that, when a grammar is LL, marker nonterminals can be added at any position in the body, and the resulting grammar will still be LR. The intuition, however, is as follows. If a grammar is LL, then we can determine that a string w on the input is derived from nonterminal A, in a derivation that starts with production A → α, by seeing only the first symbol of w (or the following symbol if w = ε). Thus, if we parse w bottom-up, then the fact that a prefix of w must be reduced to α and then to S is known as soon as the beginning of w appears on the input. In particular, if we insert markers anywhere in α, the LR states will incorporate the fact that this marker has to be there, and will reduce ε to the marker at the appropriate point on the input.

Before we discuss the actions that are associated with markers *M* and *N*, let us outline the “inductive hypothesis” about where attributes are stored.

- 1. Below the entire body of the while-production — that is, below **while** on the stack — will be the inherited attribute *S.next*. We may not know the nonterminal or parser state associated with this stack record, but we can be sure that it will have a field, in a fixed position of the record, that holds *S.next* before we begin to recognize what is derived from this *S*.
- 2. Inherited attributes *C.true* and *C.false* will be just below the stack record for *C*. Since the grammar is presumed to be LL, the appearance of **while** on the input assures us that the while-production is the only one that can be recognized, so we can be sure that *M* will appear immediately below *C* on the stack, and *M*’s record will hold the inherited attributes of *C*.
- 3. Similarly, the inherited attribute *S₁.next* must appear immediately below *S₁* on the stack, so we may place that attribute in the record for *N*.
- 4. The synthesized attribute *C.code* will appear in the record for *C*. As always when we have a long string as an attribute value, we expect that in practice a pointer to (an object representing) the string will appear in the record, while the string itself is outside the stack.
- 5. Similarly, the synthesized attribute *S₁.code* will appear in the record for *S₁*.
