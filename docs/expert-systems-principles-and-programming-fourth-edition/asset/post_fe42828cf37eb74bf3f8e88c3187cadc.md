
- 12.9 Add rules to print a message in the warnings phase to indicate that a sensor has had normal status for at least n cycles, where the number n is specified in a fact. Print the message only every nth cycle.

- 12.10 How could the backward-chaining rules in Section 12.4 be modified to allow forward chaining?

- 12.11 Modify the program developed for Problem 11.1 on page 702 so that the facts representing the shrubs are loaded from a file using the load-facts function. After explanations are provided, the user should be queried to determine whether another shrub selection is desired, and, if so, the program should be run again.

- 12.12 Using the program developed for Problem 11.3, modify the program developed for Problem 10.10 on page 620 so that only the gizmos that have not been selected are listed in the “Add Gizmo” submenu and only the gizmos that have been selected are listed in the “Remove Gizmo” submenu. In the main menu, the “Add Gizmo” menu choice should appear only if there are unselected gizmos, and the “Remove Gizmo” menu choice should appear only if there are selected gizmos.

- 12.13 Using the program developed for Problem 11.3 on page 702, modify the program developed for Problem 10.4 on page 618 to use a menu-driven interface. The user should be provided with separate menu options for specifying the color, hardness, and density of the gem being identified. Specification of the color should be done using a submenu containing the valid colors. A menu option should be provided that lists the gems satisfying the currently specified criterion. For example, if the user has only specified that the gem is black, the selection of this menu option will list only gems that can be black. Two other menu options should be provided, one that lists the current values specified for the criterion and another that resets all of the criteria to an unspecified state.

## BIBLIOGRAPHY

(Firebaugh 88). Morris W. Firebaugh, Artificial Intelligence: A Knowledge-Based Approach, Boyd & Fraser Publishing, p. 309, 1988.

## APPENDIX A
Some Useful Equivalences

p ≡ p
p → q ≡ ¬p ∨ q ≡ ¬q → ¬p
¬(p ∧ q) ≡ ¬p ∨ ¬q
¬(p ∨ q) ≡ ¬p ∧ ¬q
p ∧ (q ∨ r) ≡ (p ∧ q) ∨ (p ∧ r)
p ∨ (q ∧ r) ≡ (p ∨ q) ∧ (p ∨ r)
(p ∧ q) ∧ r ≡ p ∧ (q ∧ r)
(p ∨ q) ∨ r ≡ p ∨ (q ∨ r)
p ∧ q ≡ q ∧ p
p ∨ q ≡ q ∨ p

¬(∀x) P(x) ≡ (∃x) ¬P(x)
¬(∃x) P(x) ≡ (∀x) ¬P(x)
(∀x) P(x) ∧ (∀x) Q(x) ≡ (∀x) (P(x) ∧ Q(x))
(∃x) P(x) ∨ (∃x) Q(x) ≡ (∃x) (P(x) ∨ Q(x))

Note: The ∀ does not distribute over an ∨, and ∃ does not distribute over ∧, so a new dummy variable, z, is needed in the following two equivalences.

(∀x) P(x) ∨ (∀x) Q(x) ≡ (∀x) P(x) ∨ (∀z) Q(z)
≡ (∀x) (∀z) (P(x) ∨ Q(z))
(∃x) P(x) ∧ (∃x) Q(x) ≡ (∃x) P(x) ∧ (∃z) Q(z)
≡ (∃x) (∃z) (P(x) ∧ Q(z))

## APPENDIX B
Some Elementary Quantifiers and Their Meanings

| Formula | Meaning |
| :--- | :--- |
| (∀ x) (P(x) → Q(x)) | For all x, all P are Q |
| (∀ x) (P(x) → ¬Q(x)) | For all x, no P are Q |
| (∃ x) (P(x) ∧ Q(x)) | For some x, x are P and Q |
| (∃ x) (P(x) ∧ ¬Q(x)) | For some x, x are P and not Q |
| (∀ x) P(x) | For all x, x is P |
| (∃ x) P(x) | Some x is P (or there are P) |
| ¬(∀ x) P(x) | Not all x are P (or some x are P) |
| (∀ x) ¬P(x) | All x are not P |
| (∀ x) (∃ y) P(x,y) | For all x, there is a y such that P |
| (∃ x) ¬P(x) | Some x is not P |

## APPENDIX C
Some Set Properties

| Property | Formula |
| :--- | :--- |
| Commutativity | \( A \cup B = B \cup A \)<br>\( A \cap B = B \cap A \) |
| Associativity | \( A \cup (B \cup C) = (A \cup B) \cup C \)<br>\( A \cap (B \cap C) = (A \cap B) \cap C \) |
| Idempotence | \( A \cup A = A \)<br>\( A \cap A = A \) |
| Distributivity | \( A \cup (B \cap C) = (A \cup B) \cap (A \cup C) \)<br>\( A \cap (B \cup C) = (A \cap B) \cup (A \cap C) \) |
| Law of the Excluded Middle | \( A \cup A' = U \) |
| Law of Contradiction | \( A \cap A' = \emptyset \) |
| Identity | \( A \cup \emptyset = A \)<br>\( A \cap U = A \) |
| Absorption | \( A \cup (A \cap B) = A \)<br>\( A \cap (A \cup B) = A \) |
| de Morgan's Laws | \( (A \cap B)' = A' \cup B' \)<br>\( (A \cup B)' = A' \cap B' \) |
| Involution | \( (A')' = A \) |
| Equivalence | \( (A' \cup B) \cap (A \cup B') = (A' \cap B') \cup (A \cap B) \) |
| Symmetrical Difference | \( (A' \cap B) \cup (A \cap B') = (A' \cup B') \cap (A \cup B) \) |

## APPENDIX D CLIPS Support Information

The CD-ROM included with this book contains CLIPS 6.22 executables for MS-DOS, Windows 2000/XP, and MacOS X. Also included on the CD-ROM are all of the CLIPS source code, the three-volume CLIPS Reference Manual, and the CLIPS User's Guide. Volume I of the CLIPS Reference Manual, The Basic Programming Guide, provides the definitive description of CLIPS syntax and examples of usage. Volume II, The Advanced Programming Guide, provides details on customizing CLIPS, adding new functions to CLIPS, embedding CLIPS, and other advanced features. Volume III, The Interfaces Guide, provides information on the environment-specific interfaces for CLIPS. An X Windows version of CLIPS can be created by compiling the X Windows interface and CLIPS source code found on the CD-ROM.

Bug fixes, updates, and other information related to CLIPS can be found at the CLIPS home page at http://www.ghg.net/clips/CLIPS.html. Questions regarding CLIPS can be sent via electronic mail to clipsYYYY@ghg.net where YYYY is the current year (for example, 2004). Usenet users can find information and post questions about CLIPS at the comp.ai.shells news group.

The CLIPS Developers' Forum, located at http://www.cpbinc.com/clips, is a thread-based message board that provides a site for discussion of research, development, and implementation of the CLIPS Expert System and related technologies.

An electronic conferencing facility is also available to CLIPS users. Subscribers to this facility may send questions, observations, answers, editorials, and so forth in the form of electronic mail to the conference. All subscribers will have a copy of these messages reflected back to them at their respective email addresses. To subscribe, send a single line message to clips-request@discmsys.com containing the word "subscribe". The subject field is ignored but the address found in the "Reply:", "Reply to:", or "From:" field will be entered in the distribution list. Upon subscription you will receive a mail message instructing you how to participate in the conference from that point forward.

## APPENDIX E CLIPS Commands and Functions Summary

### Agenda

- `(agenda [<module-name>])`
  Lists the activations on the agenda of the specified module (or in the current module if `<module-name>` is unspecified).

- `(clear-focus-stack)`
  Returns all the module names from the focus stack.

- `(focus <module-name>+)`
  Pushes one or more modules onto the focus stack. The specified modules are pushed onto the focus stack in the reverse order from the argument list.

- `(get-focus)`
  Returns the module name of the current focus.

- `(get-focus-stack)`
  Returns all the module names in the focus stack as a multifield value.

- `(get-salience-evaluation)`
  Returns the current salience evaluation behavior.

- `(get-strategy)`
  Returns the current conflict resolution strategy.

- `(halt)`
  Stops the execution of rules.

- `(list-focus-stack)`
  Lists all the module names on the focus stack.

- `(pop-focus)`
  Returns the module name of the current focus and removes the current focus from the focus stack.

- `(refresh-agenda [<module-name>])`
  Forces reevaluation of the salience of rules on the agenda of the specified module (or in the current module if `<module-name>` is unspecified).

```
(run [<integer-expression>])
```

Starts the execution of rules in the current focus. If <integer-expression> is specified then only that number of rules is executed, otherwise execution halts when the agenda is empty.

```
(set-salience-evaluation <behavior>)
<behavior> ::= when-defined | when-activated |
every-cycle
```

Sets the salience evaluation behavior.

```
(set-strategy <strategy>)
<strategy> ::= depth | breadth | simplicity |
complexity | lex | mea | random
```

Sets the current conflict resolution strategy.

### Basic Math

```
(abs <numeric-expression>)
```

Returns the absolute value of its only argument.

```
(div <numeric-expression> <numeric-expression>+)
```

Returns the value of the first argument divided by each of the subsequent arguments. Division is performed using integer arithmetic.

```
(float <numeric-expression>)
```

Returns its only argument converted to type float.

```
(integer <numeric-expression>)
```

Returns its only argument converted to type integer.

```
(max <numeric-expression> <numeric-expression>+)
```

Returns the value of its largest argument.

```
(min <numeric-expression> <numeric-expression>+)
```

Returns the value of its smallest argument.

```
(+ <numeric-expression> <numeric-expression>+)
```

Returns the sum of its arguments.

```
(- <numeric-expression> <numeric-expression>+)
```

Returns the value of the first argument minus the sum of all subsequent arguments.

```
(* <numeric-expression> <numeric-expression>+)
```

Returns the product of its arguments.

```
(/ <numeric-expression> <numeric-expression>+)
```

Returns the value of the first argument divided by each of the subsequent arguments.

### Conversion

```
(deg-grad <numeric-expression>)
```

Returns the value of its argument converted from units of degrees to units of gradients.

```
(deg-rad <numeric-expression>)
```

Returns the value of its argument converted from units of degrees to units of radians.

```
(exp <numeric-expression>)
```

Returns the value of e raised to the power of its only argument.

```
(grad-deg <numeric-expression>)
```

Returns the value of its argument converted from units of gradients to units of degrees.
