
### 8.4 Given a series of facts describing shapes using the following deftemplates:

```
(deftemplate square
  (slot id) (slot side-length))
(deftemplate rectangle
  (slot id) (slot width) (slot height))
(deftemplate circle
  (slot id) (slot radius))
```

write one or more rules that will compute the sum of:

- (a) the areas of the shapes.
- (b) the perimeters of the shapes.

Test the output of the rules with the following deffacts:

```
(deffacts test-8-8
  (square (id A) (side-length 3))
  (square (id B) (side-length 5))
  (rectangle (id C) (width 5) (height 7))
  (circle (id D) (radius 2))
  (circle (id E) (radius 6)))
```

### 8.5 Given information about the name, eye color, hair color, and nationality of a person from a group using the following deftemplate:

```
(deftemplate person
  (slot name)
  (slot eye-color)
  (slot hair-color)
  (slot nationality))
```

write one rule that will identify:

- (a) anyone with blue or green eyes who has brown hair and is from France.
- (b) anyone who does not have blue eyes or black hair and does not have the same color hair and eyes.
- (c) two people, the first having brown or blue eyes, not having blond hair, and a German nationality; the second having green eyes, the same hair color as the first person, and any nationality. The second person's eyes may be brown if the first person's hair is brown.

### 8.6 Convert the following infix expressions to prefix expressions:

- (a) ( ( 3 + 4 ) * ( 5 + 6 ) + 7
- (b) ( 5 * ( 5 + 6 + 7 ) - ( ( 3 * ( 4 / 9 ) + 2 ) / 8)
- (c) 6 - 9 * 8 / 3 + 4 - (8 - 2 - 3) * 6 / 7

### 8.7 Consider the following information about a baseball team. Andy dislikes the catcher. Ed's sister is engaged to the second baseman. The center fielder is taller than the right fielder. Harry and the third baseman live in the same building. Paul and Allen each won $20 from the pitcher at pinochle. Ed and the outfielders play poker during their free time. The pitcher's wife is the third baseman's sister. All the battery (the pitcher and catcher) and infield, except Allen, Harry, and Andy, are shorter than Sam. Paul, Andy, and the shortstop each lost $50 at the racetrack. Paul, Harry, Bill, and the catcher took a trouncing from the second baseman at pool. Sam was involved in a divorce. The catcher and the third baseman each have two children. Ed, Paul, Jerry, the right fielder, and the center fielder are bachelors; the others are married. The shortstop, the third baseman, and Bill each cleaned up $100 betting on a fight. One of the outfielders is either Mike or Andy. Jerry is taller than Bill. Mike is shorter than Bill. Each of them is heavier than the third baseman. Sam, the catcher, and the third baseman are left-handed. Ed, Sam, and the shortest went to high school together. Write a CLIPS program to determine who plays each position.

### 8.8 Convert the decision tree shown in Figure 3.3 on page 99 to a series of CLIPS rules. Create patterns to match facts using the following deftemplate:

```
(deftemplate question
 (slot query-string)
 (slot answer))
```

For example, if the answer to the question represented by the root node in the tree was “no,” the fact representing this information would be:

```
(question (query-string “Is it very big?”)
 (answer no))
```

Use the printout and read functions on the RHS of the rules to ask the questions shown in Figure 3.3 and assert question facts with the user’s response.

### 8.9 Write a CLIPS program that will add two binary numbers without using any arithmetic functions. Represent the binary numbers using the following deftemplate:

```
(deftemplate binary-#
 (multislot name)
 (multislot digits))
```

Given a fact indicating which two named binary numbers are to be added, the program should create a new named binary number containing the sum. For example, the facts:

```
(binary-# (name A) (digits 1 0 1 1 1))
(binary-# (name B) (digits 1 1 1 0))
(add-binary-#s (name-1 A) (name-2 B))
```

should cause the following fact to be added to the fact list:

```
(binary-# (name (A + B)) (digits 1 0 0 1 0 1))
```

### 8.10 Write a CLIPS program that prompts for the blood types of a patient in need of a blood transfusion and a donor. The program should then determine whether the transfusion should proceed based on the blood types. Type O blood can be transfused only with type O blood. Type A blood can be transfused with either type A or type O blood. Type B blood can be transfused with either type B or type O blood. Type AB blood can be transfused with type AB, type A, type B, or type O blood.

### 8.11 Write a CLIPS program that gives information on either how a specified cut of beef can be cooked or the cuts of beef that can be cooked in a specific way. The program should first prompt whether a cut of beef or a method of cooking is to be selected and then it should prompt for an appropriate selection. Use the following guidelines to determine the appropriate cuts or methods of cooking: rump roast should be braised or roasted; sirloin steak should be broiled, pan-broiled, or pan-fried; T-bone steak should be broiled, pan-broiled, or pan-fried; rib roast should be roasted; ground beef should be roasted, broiled, pan-broiled, pan-fried, or braised; flank steak should be braised; and round steak should be braised.

### 8.12 Modify the program developed for Problem 7.14 on page 363 so that the input is determined by asking the user a series of questions regarding the necessary characteristics of the shrub. The output of the program should be the same.

### 8.13 Bacteria can be classified by several characteristics including their basic shape (spherical, rod, spiral, or filamentous), the results of a laboratory gram stain test (positive, negative, or none), and whether they require oxygen to survive (aerobic or anaerobic). Write a program that identifies the bacterial type based on the information stored in the table below. The program should ask the user for the shape, gram stain, and oxygen requirements of the bacteria. The user should be able to specify that any of the inputs is unknown. The output of the program should be all of the possible bacteria types based on the information from the user.

| Type | Shape | Gram Stain | Oxygen Requirements |
| :--- | :--- | :--- | :--- |
| Actinomycete | rod or filamentous | positive | aerobic |
| Coccoid | spherical | positive | aerobic and anaerobic |
| Coryneform | rod | positive | aerobic |
| Endospore-forming | rod | positive or negative | aerobic and anaerobic |
| Enteric | rod | negative | aerobic |
| Gilding | rod | negative | aerobic |
| Mycobacterium | spherical | none | aerobic |
| Mycoplasma | spherical | none | aerobic |
| Pseudomonad | rod | negative | aerobic |
| Rickettsia | spherical or rod | negative | aerobic |
| Sheathed | filamentous | negative | aerobic |
| Spirillum | spiral | negative | aerobic |
| Spirochete | spiral | negative | anaerobic |
| Vibrio | rod | negative | aerobic |

### 8.14 Acme Electronics makes a device called the Thingamabob 2000. This device is available in five different models distinguished by the chassis. Each chassis provides a number of bays for optional gizmos and is capable of generating a certain amount of power. The following table summarizes the chassis attributes:

| Chassis | Gizmo Bays Provided | Power Provided | Price ($) |
| :--- | :--- | :--- | :--- |
| C100 | 1 | 4 | 2000.00 |
| C200 | 2 | 5 | 2500.00 |
| C300 | 3 | 7 | 3000.00 |
| C400 | 2 | 8 | 3000.00 |
| C500 | 4 | 9 | 3500.00 |

Each gizmo that can be installed in the chassis requires a certain amount of power to operate. The following table summarizes the gizmo attributes:

| Gizmo | Power Used | Price ($) |
| :--- | :--- | :--- |
| Zaptron | 2 | 100.00 |
| Yatmizer | 6 | 800.00 |
| Pherenator | 1 | 300.00 |
| Malicifier | 3 | 200.00 |
| Zeta-shell | 4 | 150.00 |
| Warmosynchronizer | 2 | 50.00 |
| Dynoseparator | 3 | 400.00 |

Given as input facts representing the chassis and any gizmos that have been selected, write a program that generates facts representing the number of gizmos used, the total amount of power required for the gizmo, and the total price of the chassis and all gizmos selected.

### 8.15 Using the gem table from Problem 7.13 on page 363, write rules for identifying the following gems: diamond, corundum, chrysoberyl, spinel, quartz, and tourmaline. Include rules to query the user for the hardness, density, and color of the gem. The user should be prompted until he or she responds with one of the colors listed in the table.

### 8.16 Add rules to the Sticks program that will ask if the human player wants to play again after the game has finished.

### 8.17 Modify the Sticks program to allow two human players to play the game against each other, in addition to the computer playing against a human.

### 8.18 Rewrite the following rules as a single rule using and and or CEs:

```
(defrule rule-1
(fact-a)
(fact-d)
=>)
```

```
(defrule rule-2
(fact-b)
(fact-c)
(fact-e)
(fact-f)
=>)
```

```
(defrule rule-3
(fact-a)
(fact-e)
(fact-f)
=>)
```

```
(defrule rule-4
(fact-b)
(fact-c)
(fact-d)
=>)
```

### 8.19 Write a program using and and or CEs for the AND/OR tree of getting to work shown in Figure 3.10 on page 107. Test it for all branches.

### 8.20 Determine whether the variable x is referenced properly for each of the following rules. Explain your answers.

```
(a) (defrule example-1
(not (fact ?x))
(test (> ?x 4))
=>)
```

```
(b) (defrule example-2
(not (fact ?x (:> ?x 4)))
=>)
```
