are dealing with reproducible events or subjective probabilities. For simplicity, we'll use the term probability for uncertainties.

The different situations can be classified on whether the evidence is certain or uncertain and whether there is simple evidence or compound evidence. Simple evidence consists of a single piece of evidence such as:

```
IF the transmission is bad
THEN repair the car
```

while compound evidence consists of multiple pieces of evidence usually linked by AND connections, as in:

```
IF the transmission is bad AND
the engine is bad
THEN sell the car
```

or expressed formally:

```
IF E1 and E2 then H
```

We may assign a probability to this rule such as P(H | E1 ∩ E2) = 0.80, which means we are 80% sure the car should be sold on the basis of this evidence.

A further refinement of the evidence is determining its probability. For example: probability of the transmission being bad may depend on two symptoms:

+   (a) Transmission fluid is leaking
+   (b) The car jerks when changing gears

These observations lead to a probability of the transmission evidence. For example, on the basis of symptoms (a) and (b), we may decide:

```
P(E | e) = 0.95
where E = transmission is bad
e = symptoms (a) and (b) above
```

Now let's examine in more detail the probabilities associated with the different situations.

Situation 1: One piece of known evidence concludes H.

This is the simplest case with rules of the form:

```
IF E THEN H
```