
## 5.4. SYNTAX-DIRECTED TRANSLATION SCHEMES

$B \rightarrow B_1\ B_2 \mid [B_1\ \text{sub}\ B_2] \mid (B_1) \mid \text{text}$

Corresponding to these four productions, a box can be either

- 1. Two boxes, juxtaposed, with the first, $B_1$, to the left of the other, $B_2$.
- 2. A box and a subscript box. The second box appears in a smaller size, lower, and to the right of the first box.
- 3. A parenthesized box, for grouping of boxes and subscripts. Eqn and \TeX both use curly braces for grouping, but we shall use ordinary, round parentheses to avoid confusion with the braces that surround actions in SDT’s.
- 4. A text string, that is, any string of characters.

This grammar is ambiguous, but we can still use it to parse bottom-up if we make subscripting and juxtaposition right associative, with **sub** taking precedence over juxtaposition.

Expressions will be typeset by constructing larger boxes out of smaller ones. In Fig. 5.24, the boxes for $E_1$ and $height$ are about to be juxtaposed to form the box for $E_1.height$. The left box for $E_1$ is itself constructed from the box for $E$ and the subscript 1. The subscript 1 is handled by shrinking its box by about 30%, lowering it, and placing it after the box for $E$. Although we shall treat $height$ as a text string, the rectangles within its box show how it can be constructed from boxes for the individual letters.

![](img/2a44b9071782fade81f3050c3b718341_336_0.png)

Figure 5.24: Constructing larger boxes from smaller ones

In this example, we concentrate on the vertical geometry of boxes only. The horizontal geometry — the widths of boxes — is also interesting, especially when different characters have different widths. It may not be readily apparent, but each of the distinct characters in Fig. 5.24 has a different width.

The values associated with the vertical geometry of boxes are as follows:

- a) The *point size* is used to set text within a box. We shall assume that characters not in subscripts are set in 10 point type, the size of type in this book. Further, we assume that if a box has point size $p$, then its subscript box has the smaller point size $0.7p$. Inherited attribute $B.ps$ will represent the point size of box $B$. This attribute must be inherited, because the context determines how much a given box needs to be shrunk, due to the number of levels of subscripting.
- b) Each box has a *baseline*, which is a vertical position that corresponds to the bottom lines of lines of text, not counting any letters, like “g” that extend below the normal baseline. In Fig. 5.24, the dotted line represents the baseline for the boxes *E*, *height*, and the entire expression. The baseline for the box containing the subscript 1 is adjusted to lower the subscript.
- c) A box has a *height*, which is the distance from the top of the box to the baseline. Synthesized attribute *B.ht* gives the height of box *B*.
- d) A box has a *depth*, which is the distance from the baseline to the bottom of the box. Synthesized attribute *B.dp* gives the depth of box *B*.

The SDD in Fig. 5.25 gives rules for computing point sizes, heights, and depths. Production 1 is used to assign *B.ps* the initial value 10.

| Production | Semantic Rules |
|---|---|
| 1) $S \to B$ | $B.ps = 10$ |
| 2) $B \to B_1\ B_2$ | $B_1.ps = B.ps$<br>$B_2.ps = B.ps$<br>$B.ht = \max(B_1.ht, B_2.ht)$<br>$B.dp = \max(B_1.dp, B_2.dp)$ |
| 3) $B \to B_1\ \mathrm{sub}\ B_2$ | $B_1.ps = B.ps$<br>$B_2.ps = 0.7 \times B.ps$<br>$B.ht = \max(B_1.ht, B_2.ht - 0.25 \times B.ps)$<br>$B.dp = \max(B_1.dp, B_2.dp + 0.25 \times B.ps)$ |
| 4) $B \to (\ B_1\ )$ | $B_1.ps = B.ps$<br>$B.ht = B_1.ht$<br>$B.dp = B_1.dp$ |
| 5) $B \to \mathrm{text}$ | $B.ht = \mathrm{getHt}(B.ps, \mathrm{text.lexval})$<br>$B.dp = \mathrm{getDp}(B.ps, \mathrm{text.lexval})$ |

Production 2 handles juxtaposition. Point sizes are copied down the parse tree; that is, two sub-boxes of a box inherit the same point size from the larger box. Heights and depths are computed up the tree by taking the maximum. That is, the height of the larger box is the maximum of the heights of its two components, and similarly for the depth.

Production 3 handles subscripting and is the most subtle. In this greatly simplified example, we assume that the point size of a subscripted box is 70% of the point size of its parent. Reality is much more complex, since subscripts cannot shrink indefinitely; in practice, after a few levels, the sizes of subscripts

## SONiC System Architecture

SONiC (Software for Open Networking in the Cloud) is an open-source network operating system based on Linux. It runs on commercial ASICs from multiple vendors and provides a full-suite of network functionality that has been production-hardened in the data centers of the world's largest cloud service providers. This page explains the SONiC architecture.

The figure below shows the high-level architecture of SONiC that offers flexibility to support multiple ASICs and multiple hardware platforms.

![](img/2a44b9071782fade81f3050c3b718341_338_0.png)

### Containerized SONiC Components

SONiC is composed of multiple docker-based containers. The key components in the SONiC architecture include:

- **Teamd** containerizes the teamd protocol for link aggregation (LAG).
- **FPM (Forwarding Plane Manager)** containerizes the BGP and other routing protocol stacks.
- **SNMP** containerizes the SNMP server.
- **DHCP Relay** containerizes DHCP relay functionality.
- **LLDP** containerizes the Link Layer Discovery Protocol.
- **Pmon** containerizes platform monitoring services.
- **NAT** containerizes network address translation functionality.

## 5.4. SYNTAX-DIRECTED TRANSLATION SCHEMES

expression “on-the-fly,” rather than computing it as an attribute. However, in our first formulation, we create a string-valued attribute by concatenation.

**Example 5.19:** For this example, we only need one production:

$$S \to \text{while }(C)\ S_1$$

Here, $S$ is the nonterminal that generates all kinds of statements, presumably including if-statements, assignment statements, and others. In this example, $C$ stands for a conditional expression — a boolean expression that evaluates to true or false.

In this flow-of-control example, the only things we ever generate are labels. All the other intermediate-code instructions are assumed to be generated by parts of the SDT that are not shown. Specifically, we generate explicit instructions of the form label $L$, where $L$ is an identifier, to indicate that $L$ is the label of the instruction that follows. We assume that the intermediate code is like that introduced in Section 2.8.4.

The meaning of our while-statement is that the conditional $C$ is evaluated. If it is true, control goes to the beginning of the code for $S_1$. If false, control goes to the code that follows the while-statement’s code. The code for $S_1$ must be designed to jump to the beginning of the code for the while-statement when finished; the jump to the beginning of the code that evaluates $C$ is not shown in Fig. 5.27.

We use the following attributes to generate the proper intermediate code:

- 1. The inherited attribute $S.next$ labels the beginning of the code that must be executed after $S$ is finished.
- 2. The synthesized attribute $S.code$ is the sequence of intermediate-code steps that implements a statement $S$ and ends with a jump to $S.next$.
- 3. The inherited attribute $C.true$ labels the beginning of the code that must be executed if $C$ is true.
- 4. The inherited attribute $C.false$ labels the beginning of the code that must be executed if $C$ is false.
- 5. The synthesized attribute $C.code$ is the sequence of intermediate-code steps that implements the condition $C$ and jumps either to $C.true$ or to $C.false$, depending on whether the condition is true or false.

The SDD that computes these attributes for the while-statement is shown in Fig. 5.27. A number of points merit explanation:

- The function $new$ generates new labels.
- The variables $L_1$ and $L_2$ hold labels that we need in the code. $L_1$ is the beginning of the code for the while-statement, and we need to arrange
