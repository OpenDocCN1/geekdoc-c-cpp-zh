where FA₁₆ is the opcode, 4 is the first 4 bit length code (one less than 5, as before), 2 is the second length, D is the first base, 020₁₆ is the first displacement, D is the second base and 040₁₆ is the second displacement.

# 6.7.5.3 Added SS Formats

In later versions of the architecture additional SS formats were added as shown in Figure 15. These tend to be uncommon instructions such as Load Multiple Disjoint (LMD), Shift and Round Decimal (SRP), Move to Primary (MVCP), Move to Secondary (MVCS) and Move With Key (MVCK).

![](bbox=[0.15, 0.36, 0.95, 0.62])

Figure 15 Newer SS Formats

# 6.8 Newer Instruction Formats

As time passed, the architecture evolved. The original 24 bit (16 megabyte) address space grew to 31 bits (2 gigabytes) and then to 64 bits (16 exabytes); the original 32 bit general purpose registers became 64 bits and so on. To take advantage of these changes, instructions were added along with new instruction formats. A good example of what happened can be seen in the evolution of the signed, fixed point binary Add instruction.

In the original architecture there were three instructions you could use to add signed binary integers as shown in Table 12. The first two of these, AR and A, add two 32 bit signed fixed point binary values yielding a 32 bit signed fixed point binary result. The AH instruction adds a 16 bit signed fixed point binary value to a 32 bit register value and yields a signed 32 bit binary result.

| Mnemonic | Format | 1st | 2nd | 2nd Operand | Result | Op |
|---|---|---|---|---|---|---|