concatenated coding system with the inner encoder consisting of either a (2, 1, 6, 10) or (3, 1, 6, 15) convolutional code. The (2, 1, 6, 10) code has generator matrix [g1(D) g2(D)], where

```
g_1(D) = 1 + D + D^3 + D^4 + D^6.
g_2(D) = 1 + D^3 + D^4 + D^5 + D^6.
```

The (3, 1, 6, 15) code has generator matrix [g1(D) g2(D) g3(D)], where g1(D) and g2(D) are as above and g3(D) = 1 + D^2 + D^4 + D^5 + D^6. At a BER of 1 x 10^-5, the (2, 1, 6, 10) code provides a coding gain of 5.4 dB, and the (3, 1, 6, 15) code provides a coding gain of 5.7 dB. Both codes can be decoded efficiently using the Viterbi Algorithm but the (2, 1, 6, 10) code has become the preferred choice.

Voyager 1 and 2 were launched in the summer of 1977 destined to explore Jupiter, Saturn, and their moons. These spacecraft transmitted two different types of data: imaging and GSE (general science and engineering). The imaging system required less reliability than the GSE system and used the (2, 1, 6, 10) code for its encoding. The GSE data was transmitted using a concatenated code. The outer encoder was the [24, 12, 8] extended binary Golay code. After encoding using the binary Golay code, codeword interleaving was performed with the result passed to the inner encoder, which was the (2, 1, 6, 10) code. The process was reversed in decoding. (The imaging data merely bypassed the Golay code portion of the encoding and decoding process.) Partially because of the effective use of coding, NASA engineers were able to extend the mission of Voyager 2 to include flybys of Uranus and Neptune. To accomplish this, the GSE data was transmitted using a concatenated code with outer encoder to a [256, 224, 33] Reed-Solomon code over F256, in place of the Golay code, followed by the (2, 1, 6, 10) inner encoder. Later NASA missions, including Galileo and some European Space Agency (ESA) missions such as the Giotto mission to Halley's Comet, used similar error-correction coding involving a Reed-Solomon code and a convolutional code with the added step of interleaving after encoding with the Reed-Solomon code. The coding gain for the Voyager coding system is shown in Figure 15.11.

The Galileo mission to study Jupiter and its atmosphere was fraught with problems from the outset. Originally scheduled for launch from the space shuttle in early 1986, the mission was delayed until late 1989 due to the shuttle Challenger in-flight explosion on January 28, 1986. Galileo was launched with two different concatenated codes. The outer encoder of both systems was the (256, 224, 33) Reed-Solomon code. The inner encoder for one system was the (2, 1, 6, 10) CCSDS standard code, while the inner encoder for the other was a (4, 1, 14) convolutional code with generator matrix [g1(D) g2(D) g3(D) g4(D)], where

```
g_1(D) = 1 + D^3 + D^4 + D^7 + D^8 + D^{10} + D^{14},
g_2(D) = 1 + D^2 + D^5 + D^7 + D^9 + D^{10} + D^{11} + D^{14},
g_3(D) = 1 + D + D^4 + D^5 + D^6 + D^7 + D^9 + D^{10} + D^{12} + D^{13} + D^{14},
g_4(D) = 1 + D + D^2 + D^6 + D^8 + D^{10} + D^{11} + D^{12} + D^{14}.
```

At each time increment, the Viterbi decoder for the (4, 1, 14) code had to examine 2^14 = 16 384 states. To accomplish this daunting task, JPL completed the Big Viterbi Decoder in