label L2, and finally the code from the recursive call to S (which is the same as $S_{code}$ in Fig. 5.29). Thus, the code printed by this call to S is exactly the same as the return value in Fig. 5.29. □

Incidentally, we can make the same change to the underlying SDT: turn the construction of a main attribute into actions that emit the elements of that attribute. In Fig. 5.32 we see the SDT of Fig. 5.28 revised to generate code on the fly.

```
```
S → while ( { L1 = new(); L2 = new(); C.false = S.next;
                C.true = L2; print("label1",L1); }
        C )    { S1.next = L1; print("label1",L2); }
        S1
```
```

Figure 5.32: SDT for on-the-fly code generation for while statements

# 5.5.3 L-Attributed SDD's and LL Parsing

Suppose that an L-attributed SDD is based on an LL-grammar and that we have converted it to an SDT with actions embedded in the productions, as described in Section 5.4.5. We can then perform the translation during LL parsing by extending the parser stack to hold actions and certain data items needed for attribute evaluation. Typically, the data items are copies of attributes.

In addition to records representing terminals and nonterminals, the parser stack will hold action-records representing actions to be executed and synthesize-records to hold the synthesized attributes for nonterminals. We use the following two principles to manage attributes on the stack:

+   - The inherited attributes of a nonterminal $A$ are placed in the stack record that represents that nonterminal. The code to evaluate these attributes will usually be represented by an action-record immediately above the stack record for $A$; in fact, the conversion of L-attributed SDD's to SDT's ensures that the action-record will be immediately above $A$.
+   - The synthesized attributes for a nonterminal $A$ are placed in a separate synthesize-record that is immediately below the record for $A$ on the stack.

This strategy places records of several types on the parsing stack, trusting that these variant record types can be managed properly as subclasses of a “stack-record” class. In practice, we might combine several records into one, but the ideas are perhaps best explained by separating data used for different purposes into different records.

Action-records contain pointers to code to be executed. Actions may also appear in synthesize-records; these actions typically place copies of the synthesized attribute(s) in other records further down the stack, where the value of