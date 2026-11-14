# 19.4.2 Programmable Array Logic – PAL

In the PAL or Programmable Array Logic device, the AND portion of the device is programmable and the OR portion is fixed. Such an architecture limits the number of product terms in the sum. Furthermore, the product terms are not reusable and must be duplicated if required. The implementation uses a fixed OR array. The output of each product term can be connected to only one OR gate. Typically, the device supports bidirectional I/O pins and tristate outputs with individual enables.

The structure of the device is shown in Figure 19.5. In the diagram, though drawn as only a single input to each device in the arrays, each supports multiple inputs. The open circles illustrate the programmable links.

![](bbox=[0.28, 0.28, 0.9, 0.55])

# 19.4.3 Programmable Logic Array – PLA

In contrast to the PAL, in the PLA as shown in Figure 19.6, both the AND and the OR portions of the device are programmable. Consequently, the product terms are reusable.

![](bbox=[0.28, 0.66, 0.9, 0.92])