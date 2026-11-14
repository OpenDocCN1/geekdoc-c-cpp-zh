The test may have any of four possible outcomes. If there is no bridge fault, the correct data will be read from each address. If there is a bridge fault, one must consider three cases: the logical 1 in the test address dominates, or the logical 0 dominates, or neither dominates. For the first case, the data written to the alias address - xxxx11 will be contaminated, and for the second, the data written to the alias address - xxxx00 will be corrupted. The third case is a bit more difficult (probably several bits, actually). If neither address bit dominates, then the data in any of the three addresses may be affected.

So far, the analysis of bridging faults has assumed a voltage/current model in which one of the constituent signals in the bridge dominates and, thereby, affects the logical behavior of our system. If a resistance model is considered instead, the task becomes a bit easier. With such a model, how the component operates is not important; rather, the resistance between the pins of interest is simply measured.

When formulating tests for bridging faults, one can either use a black box or a white box model. In the black box model, all possible pairs of faults must be considered. With a little knowledge about the pin out of the memory and the layout of the printed circuit board, most of the possible combinations can be eliminated. If the device pins on the bus layout are such that a bridge between two address or data lines is physically impossible, there is no need to test those combinations for such a fault.

```
groupNumber = m mod n
```

# 4.2.1.2 ROM Memory

From an external point of view, the ROM fault model is no different from that used for the RAM. In addition, the underlying assumptions on which the analysis is based are similar. For the RAM, it was assumed that the devices contained no manufacturing defects. On one level that same assumption can be made for ROMs. However, the ROM (which may be manifest as a programmable device) is intended to have a particular set of data stored. If the stored pattern is incorrect, the device is considered to have a failure. Thus, the strategy for testing ROMs must address the stuck-at and bridging faults as well as ensuring that the correct data has been stored.

CRC, cyclic redundancy check, signature analysis

An effective method for testing ROM memories that can address all of these issues is based on the CRC or cyclic redundancy check and is known as signature analysis. Signature analysis uses an LFSR to compress a data stream into a K-bit pattern. The testing algorithm is rather straightforward and follows the approach commonly used for error management in inter- and intrasystem communication.

**Design Note**

Observe that in developing a method for testing ROMs, ideas are being utilized from several different areas, areas that are completely unrelated to test. Whenever approaching a design, keep the initial options wide open and alternatives unrestricted.

One can model the contents of a ROM as an N×M bit data stream where N is the number of addresses in the ROM and M is the number of bits stored at each address or word size. To test the ROM, a CRC or signature is computed for the known data stream. A similar signature is generated for the ROM under test. If the signatures agree, the correct data has been stored; otherwise there is a data fault.