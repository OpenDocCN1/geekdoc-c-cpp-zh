
### 3.8 Prove whether the following are fallacies or rules of inference. Give an example of each.

- (a) Complex Constructive Dilemma
- p -> q
- r -> s
- p v r
- .: q v s

- (b) Complex Destructive Dilemma
- p -> q
- r -> s
- ~q v ~s
- .: ~p v ~r

- (c) Simple Destructive Dilemma
- p -> q
- p -> r
- ~q v ~r
- .: ~p

- (d) Inverse
- p -> q
- ~p
- .: ~q

### 3.9 Draw the conclusion from the following premises, taken from Lewis Carroll, author of the famous Alice's Adventures in Wonderland:

- (a) All the dated letters in this room are written on blue paper.
- (b) None of them are in black ink, except those that are written in the third person.
- (c) I have not filed any of them that I can read.
- (d) None of them that are written on one sheet, are undated.
- (e) All of them, that are not crossed, are in black ink.
- (f) All of them, written by Brown, begin with “Dear Sir”.
- (g) All of them, written on blue paper, are filed.
- (h) None of them, written on more than one sheet, are crossed.
- (i) None of them, that begin with “Dear Sir”, are written in the third person.

Hint: Use the law of contrapositives to define the following:

- A = beginning with “Dear Sir”   B = crossed   C = dated
- D = filed   E = in black ink   F = in third person
- G = letters that I can read   H = on blue paper   I = on one sheet
- J = written by Brown

### 3.10 Give a formal proof using predicate logic for the syllogism:

- No software is guaranteed
- All programs are software
- .: No programs are guaranteed

### 3.11 Use the following to write quantified first-order predicate logic formulas:
P(x) = x is a programmer
S(x) = x is smart
L(x,y) = x loves y

- (a) All programmers are smart.
- (b) Some programmers are smart.
- (c) No programmers are smart.
- (d) Someone is not a programmer.
- (e) Not everyone is a programmer.
- (f) Everyone is not a programmer.
- (g) Everyone is a programmer.
- (h) Some programmers are not smart.
- (i) There are programmers.
- (j) Everyone loves someone.

Hint: Use Appendix B.

### 3.12 Consider the predicate logic argument:
A horse is an animal.
Therefore, the head of a horse is the head of an animal. Define the following:
H(x,y) = x is the head of y
A(x) = x is an animal
S(x) = x is a horse

The premise and conclusion are as follows:
(∀ x) (S(x) → A(x))
(∀ x) ([(∃ y) (S(y) ∧ H(x,y))] → [(∃ z) (A(z) ∧ H(x,z))])

Prove the conclusion using resolution refutation. Show all nine steps in clausal conversion for the conclusion.

### 3.13
- (a) Obtain information from your bank or savings & loan on the criteria for obtaining a car loan. Write a backward-chaining system of rules to determine if an applicant should get a car loan. Be as specific as possible.
- (b) Obtain information on qualifying for a home mortgage. Give the modifications of your car loan program to handle home loans as well as car loans.
- (c) Obtain information on qualifying for a business loan. Give the modifications to the car-mortgage program to handle business loans as well.

### 3.14 Write a production system of causal rules to simulate the operation of the fuel system of your car. You may obtain this information from the repair guide for your car. Be as detailed as possible.

### 3.15 Using the repair guide for your car, write a production system that can diagnose and remedy electrical problems for your car, given symptoms of problems.

### 3.16 If the conclusion is false and you wanted to determine the facts that followed, would you use abduction or another method of inference? Explain.

### 3.17 Write IF-THEN rules to identify raspberries using the portion of the decision tree shown in Figure 3.4.

### 3.18 A parent and two children are on the left bank of a river and wish to cross to the right side. The parent weighs 200 lb and each child weighs 100 lb. One boat is available with a capacity of 200 lb. At least one person is required to row the boat. Draw the decision tree showing all the possibilities for them crossing the river and indicate the successful path through the tree so that they all cross. Assume the following operators: SL—Single child crosses from left to right SR—Single child crosses from right to left BL—Both children cross from left to right BR—Both children cross from right to left PL—Parent crosses from left to right PR—Parent crosses from right to left

### 3.19 (a) Draw a logic diagram version of the AND-exclusive-OR car decision of Figure 3.11. Note that you will have to implement the exclusive-OR using standard AND, OR, and NOT elements. (b) Write forward chaining IF-THEN rules to determine which hypothesis to follow, i.e., sell or repair.

### 3.20 What type of inference (if any) do the following statements represent? (a) “The reason I keep insisting that there was a relationship between Iraq and Saddam and al Qaeda is because there was a relationship between Iraq and al Qaeda.” (b) “It is reasonable to think that a Supreme Court justice can be bought so cheap, the nation is in deeper trouble than I had imagined.”

## BIBLIOGRAPHY

(Giarratano 93). Joseph Giarratano, CLIPS User’s Guide, NASA, Version 6.2 of CLIPS, 1993.

(Kaelbling 98). Leslie Pack Kaelbling, Michael L. Littman, and Anthony R. Cassandra, “Planning and Acting in Partially Observable Stochastic Domains,” Artificial Intelligence 101 pp. 99–134, 1998.

(Klir 98). George J. Klir and Mark J. Wierman, Uncertainty-Based Information, Physica-Verlag, 1998.

(Lakemeyer 03). ed. by Gerhard Lakemeyer and Bernhard Nebel, Exploring Artificial Intelligence in the New Millennium, Morgan Kaufmann Publishers, 2003.

(Lakoff 00). George Lakoff and Rafael E. Nunez, Where Mathematics Comes From, Basic Books, 2000.

(Merritt 04). Dennis Merritt, “Building a Custom Rule Engine with PROLOG,” Dr. Dobb’s Journal, pp. 40–45, March 2004.

(Russell 03). Stuart J. Russell and Peter Norvig, Artificial Intelligence: A Modern Approach, 2nd Edition, 2002.

## CHAPTER 4
Reasoning under Uncertainty

### 4.1 INTRODUCTION

This chapter discusses some methods of reasoning under uncertainty using probability theory and fuzzy logic. These topics are very important since one of the main strengths of an expert system is its ability to handle uncertainty just like a real person. If a satisfactory algorithm or decision tree is known, there is no need for the power of an expert system. Dealing with uncertainty is one of the main advantages of an expert system over a simple decision tree in which all the facts must be known to achieve an outcome. Probability theory is the foundation for some theories of uncertainty and so this chapter covers those elements that are relevant to probabilistic uncertainty and fuzzy logic in expert systems.

In the next chapter other theories of dealing with uncertainty will be introduced and fuzzy logic will be studied in more detail under its formal title of Approximate Reasoning. While it would be nice to have to deal with only one theory of uncertainty such as classic probability theory, there are advantages and disadvantages with each theory. This is analogous to the decisions a programmer must face in deciding what algorithm and data structure should be used in an ordinary computer program. By understanding the advantages and disadvantages of each approach to uncertainty, you will create an expert system that is best for the particular expertise being modeled. Some expert system tools have uncertainty built into the language such as two versions of CLIPS that were customized to handle fuzzy logic, the FuzzyCLIPS from the National Research Council of Canada and the Togai InfraLogic, FuzzyClips. Some other customized versions are described in the Preface.

Before using such a customized tool, you should be sure that is the correct method for uncertainty. It may be that all you need are some particular rules in which you can code the method yourself, or define an uncertainty function rather than using a whole special tool. Another possibility is that you may need to have more than one type of uncertainty modeled and there is no one tool that
