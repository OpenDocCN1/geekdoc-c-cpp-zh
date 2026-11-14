The latched or registered tristate output is shown in Figure 19.4. The output of the storage element is fed back into array from the Q output using a bipolar driver. Such an approach balances the loading on the outputs of the storage element. The polarity of the input to the storage element is controlled through the XOR device on the D input. The polarity of the output signal is controlled by selecting the state of the input signal.

![](bbox=[0.28, 0.2, 0.72, 0.34])

Figure 19.4 Simple Registered Output Configuration

The architecture of the device may require that all storage devices use the same clock and the same reset or clear signal. In the simpler devices, typically both the clock and the clear signal originate from outside the PLD device. More complex devices may also support a selection of internal or external clocking and reset sources.

# 19.4 BASIC CONFIGURATIONS

The core elements of programmable logics are found in four basic configurations:

+   - (P)ROM – (Programmable) Read Only Memory.
+   - PAL – Programmable Array Logic.
+   - PLA – Programmable Logic Array.
+   - PLS – Programmable Logic Sequencer.

# 19.4.1 The (P)ROM

The (P)ROM is the most general and flexible configuration. All combinations of the input bits are programmable.

# EXAMPLE 19.2

To use a read only memory (ROM) or PROM to implement the following logical expression:

```
F = Σ(2, 11, 12)
```

we need a 16 x 1 bit memory. Four address lines will enable each memory bit to be uniquely addressed. The equation is implemented by storing a logical 1 in addresses 2, 11, and 12 while storing a logical 0 in all remaining.

The device will have a logical 1 as an output only when those addresses (or minterms) appear on the device inputs. Each product term corresponds to 1 address.

A (P)ROM-based solution is generally appropriate only when a large number of product terms are required.