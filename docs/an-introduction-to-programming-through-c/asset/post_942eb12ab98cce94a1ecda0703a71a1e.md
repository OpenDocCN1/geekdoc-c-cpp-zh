
![](img/c7233aedab7e4c7cad32a7615b6a4783_34_0.png)

# Figure 2.2: Primary school division algorithm

Of course, algorithm design is difficult, if you are not familiar with the domain of the problem you want to solve. For example, if you want to predict the weather, you had better know differential equations and physics. So we will not consider such problems in this book. We will consider problems from more familiar domains, e.g. high school and junior college math and science, simple commerce, and of course common sense! Or if we consider unfamiliar domains, we will first present the relevant background.

## 2.2 Basic principles of digital circuits

Here is the key fact: the circuits in a computer are designed such that for practical purposes, we can pretend that numbers flow through the wires in the circuit, or get stored in the devices in the circuit. Such circuits are called digital circuits. We only discuss digital circuits in this chapter. In digital circuits, at any time instant, we can think of each individual wire as carrying a single number, or to be more precise, either the number 0 or the number 1. Likewise, there are devices, that are capable of performing a storage function (most commonly capacitors), and each such individual device can also store the number 0 or the number 1 at any time.

We briefly explain how this illusion is created. But you can ignore this paragraph if you wish, it is not needed for understanding the rest of the book. As you may know, current flows through the wires in an electrical circuit (just as water flows through pipes), and wires are associated with voltages (electrical equivalent of water pressure). The idea for representing numbers in circuits is simple: if a wire is at a certain designated high voltage (say higher than 1 volt) then we will say that the number 1 is being carried on it. If the wire is at a certain designated low voltage (say smaller than 0.2 volts), then we will say that the wire is carrying the number 0. Note further that the circuits are designed so that the wires never carry voltages in the range 0.2 volts to 1 volt, and so there is never any ambiguity. Thus we can pretend that wires in the circuit are carrying around numbers. Further note that if you store electrical charge on a capacitor, the charge does not dissipate quickly; in this sense the capacitor remembers that charge. To make the capacitor remember a 0, we simply drain off charge from it. This will happens if we connect the capacitor to our designated low voltage. If on the other hand, we connect our capacitor to a high voltage, a large amount of charge

gets stored on it; this represents the number 1. For the rest of the book, we will not worry about charges and voltages. Instead we will only talk about capacitors and wires holding and carrying the numbers 0 or 1.

Of course, we will want to store or communicate numbers besides 0 and 1. We will see how to do this in Section 2.3. Once we have numbers represented, it is possible to design circuits which can perform arithmetic on them. This is considered in Section 2.6.

## 2.3 Number representation formats

The term bit is used to denote a number which is either 0 or 1, so we will say that each wire in a computer can carry a single bit, or each capacitor can store a single bit. If we want to represent other numbers, we can do so by associating with them a sequence of bits. As an example, say we decide to associate the sequence of bits 11001 with the number 25. Then whenever we want to store 25, we will need to use 5 capacitors, and in them store the respective bits of the sequence, i.e. 1, 1, 0, 0, 1. Likewise, if we want to send the number 25 from one device to another, we must use 5 wires, and on those we must respectively send 1, 1, 0, 0, 1. The question then is, what bit sequence should we associate with each number?

The simplest idea is as follows: we represent the number using the sequence of bits given by its binary representation. So as an example, suppose we wish to represent the number 25. It has binary representation 11001. Thus it would be represented by the sequence of bits 11001, as discussed above. This idea is fine if we only wish to represent non-negative integers. It is commonly used, as we discuss in Section 2.3.1.

But our program may deal with integers which can be either positive or negative e.g. temperature rounded to the nearest degree. Thus we need a more complex scheme to represent such numbers. This is discussed in Section 2.3.2.

More generally we may have to represent quantities such as mass, force, and velocities, which in general will be real numbers, and may be either positive or negative. Schemes for representing real numbers are discussed in Section 2.3.3.

There is one more issue to consider. In the example above, we said that the number 25 could be represented by a sequence of 5 bits. On most computers, the standard representation schemes require you to choose the length of the sequence to be one of 8, 16, 32, or 64 bits. This is because restricting the size of the bit sequence to these values makes it easy to design the circuitry in the computer. Note that it is customary to use the terms byte, half-word, word, and double-word to respectively mean 8, 16, 32 and 64 bits.

### 2.3.1 Unsigned integer representation

Suppose we know that a certain quantity we deal with in our program will always be a non-negative integer, e.g. a telephone number. In that case, as discussed above, we can represent it using the sequence of bits given by its binary representation. As mentioned above, the length of the representation must be chosen to be one of 8, 16, 32, 64. Thus if the number we wish to represent has a shorter binary representation than the length we chose, then we simply make the more significant bits 0, e.g. if we wish to represent 25 using 32 bits, the representation will be the bit string

000000000000000000000000011001

Note that if we decide to use an n bit long binary representation, the maximum value that can be represented is 2^n − 1 (sequence of n 1s). Thus we must be sure that the number we wish to represent is not larger. As an example, since we know that telephone numbers (in India) are at most 8 digits long, and since the largest possible 8 digit number 99999999 < 2^32 − 1, we can use n = 32 to represent telephone numbers.

### 2.3.2 Signed integers

An integer can be negative or positive. So this throws a challenge: how do we represent negative numbers?

The simplest representation is the so called sign-magnitude representation. In this, if we have n bits to be used for representing the number, one of these is designated as a sign bit. We will set this bit to 0 if the number is positive, and to 1 if the number is negative. The remaining n − 1 bits will be used for representing the absolute value of the number. We might use the bit in the most significant position as the sign bit, so the representation for -25 using the 32 capacitors would be the bit string:

1000000000000000000000000011001

Notice that since we have decided to use n−1 bits to represent the magnitude, the magnitude can be at most 2^{n−1} − 1 (all n − 1 bits must be 1s). Since the numbers can be positive or negative, using n bits total we can represent numbers between −2^{n−1} + 1 and 2^{n−1} − 1, both inclusive.

A more commonly used representation is the so called 2’s complement representation. The n bit 2s complement representation is defined as follows. In this the integer x is represented by the n bit binary representation of the number x if 0 ≤ x ≤ 2^{n−1} − 1, and by the n bit binary representation of the number 2^n − x if −2^{n−1} ≤ x < 0. Numbers outside this range cannot be represented.

Here is how -25 would be represented in 32 bit 2’s complement representation. Since -25 is negative, we have to represent it by the binary number 2^32 − 25 = 4294967296 − 25 = 4294967271. Then we take its binary representation, which is:

1111111111111111111111111100111

Thus if you want to store -25 or send it on some wires, the above bit pattern will have to be stored or sent.

### 2.3.3 Floating point representations

Much computing needs to be done with real numbers. For example, velocities of particles, voltages, temperatures and so on in general need not take only integral values. Real numbers

2 This only means that there is no standard, built-in mechanism for representing numbers outside the range. However, you will be able to design your own mechanisms if you wish, as you are asked to in Exercise 21 of Chapter 13.

3 You may find it convenient to first convert 2^32 and 25 to binary, and then subtract.
