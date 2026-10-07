# Object Oriented Programming using C#

# The Unified Modelling Language (UML)

![](bbox=[0.148, 0.095, 0.545, 0.805])

In a University administration system we might produce a transcript of results for each year the student has studied (including a possible placement year).

This association relationship is naturally unidirectional – given a student we might want to find transcript(s), but it seems unlikely that we might have a transcript and to find the student to whom it belongs.

In a library reader can borrow up to eight books. A particular book can be borrowed by at most one reader.

We want a bidirectional relationship as here, in being able to identify all the books which a particular reader has borrowed, we might want to find the reader who has borrowed a particular book (for example to recall it in the event of a reservation).

This might be the part of the model for some kind of educational virtual anatomy program.

Composition – the “strong” relationship which shows that one object is (and has to be) part of another seems appropriate here.

The multiples would not always work for real people though – they might have lost a finger due to accident or disaster, or they have an extra one of a genetic anomaly.

But if we are modelling the “materials” in a medical school anatomy lab? A hand might not be part of a body. The “weaker” aggregation relationship would reflect this better.

A customer can have any number of bank accounts, and a bank account can be held by one person or two people (“joint account”). We suppressed the navigability of this relationship, perhaps because we have not yet decided this issue.

A bank account must either be a current or a savings account – hence Bank/Account itself is abstract.

(We could have shown this using italics rather than the <<abstract>> keyword)

Download free ebooks at bookboom.com