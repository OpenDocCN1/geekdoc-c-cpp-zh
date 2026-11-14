using the PLL. A long series of consecutive 1's will have no transitions, thus potentially resulting in a loss of sync. To solve this problem, a technique called bit stuffing is used. The USB implementation of bit stuffing in the transmitter forces a transition into an NRZI data stream whenever six consecutive 1's have been encountered. The added bits ensure that the receiver will detect a transition at least once every seventh bit time. The extra zero bit will not cause confusion at decoding, even if the seventh bit is a legitimate zero. After six 1's, the receiver knows that the next bit received will be an inserted zero and so, on receipt, discards it. The real zero will be received following and interpreted correctly.

# 18.4.10 The Physical Environment

USB connectors are designed to permit any USB peripheral device to be attached to any hub port. The USB subsystem supports two kinds of cables: low speed and high speed.

# 18.4.10.1 Low-Speed Cables

The low-speed cables, also referred to as subchannel cables, are intended only for 1.5 M byte/s signaling. The maximum cable length cannot exceed 3 m. The low-speed cables support differential pair signaling; the signal pair may be nontwisted 28 AWG stranded conductors. The low-speed cables do not require shielding.

# 18.4.10.2 High-Speed Cables

The high-speed cables require twisted shielded pair (TWSP). The maximum cable length is extended to 5 m as long as the propagation delay is less than 30 ns over the length of cable when operating in the range of 1 to 16 MHz. If such a constraint cannot be met, the cable must be shortened. Beyond the noted differences, the low- and high-speed cables are identical.

# 18.4.10.3 Cables and Cable Power

The USB cables support a limited amount of 5 VDC power that can be used by the peripheral devices. The system normally supports up to 500 mA, although it may be as little as 100 mA in certain implementations. The end view of the cable is given as illustrated in Figure 18.14.

![](bbox=[0.28, 0.65, 0.6, 0.83])

Figure 18.14 USB Cable Structure