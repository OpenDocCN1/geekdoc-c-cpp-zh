```
10:    **end if**

11:    **end for**
```

Following the *DTFNS* conversion algorithm, the representations of all decimal numbers in the range 0 to 12 (both inclusive) using four digits in TFNS are shown in Table 8.20. Note that the decimal number 8 is *uniquely* represented as 0100 in TFNS using the above conversion algorithm. Although another possible representation of the decimal number 8 in TFNS with the above positional weights could be 0022; this representation cannot be obtained by the algorithm *DTFNS* because of the *if* statement in line 3 which, in effect, forces the number to be represented by using non-zero digits at the highest possible digit positions whenever possible.

**Lemma 31.** Let *N* be a decimal number whose representation in *TFNS* is 2111⋯1 having *(k − 1)* 1’s following a 2. The decimal number *N* + 1 will be represented by 1000⋯0, with *k* 0’s after the 1.

**Proof:** From the TFNS representation of *N*, it follows that:

$$N = 2F_{2k} + F_{2k-2} + F_{2k-4} + \cdots + F_4 + F_2$$

$$\Rightarrow N + 1 = 2F_{2k} + F_{2k-2} + F_{2k-4} + \cdots + F_4 + F_2 + 1$$

$$= 2F_{2k} + F_{2k-2} + F_{2k-4} + \cdots + F_4 + F_2 + F_1$$

$$= 2F_{2k} + F_{2k-2} + F_{2k-4} + \cdots + F_6 + F_4 + F_3$$

$$= 2F_{2k} + F_{2k-2} + F_{2k-4} + \cdots + F_8 + F_6 + F_5 + \cdots$$

$$= 2F_{2k} + F_{2k-1}$$

$$= F_{2k} + F_{2k+1}$$

$$= F_{2k+2}.$$

By virtue of the conversion algorithm *DTFNS*, *N* + 1 will thus be represented as 1000⋯0 in TFNS, with *k* 0’s after the 1.