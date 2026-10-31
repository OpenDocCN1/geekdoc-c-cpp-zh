![](bbox=[0.294, 0.096, 0.748, 0.485])

Fig. 5.36. Time delay circuit according to [THOMAS et al. 1969, p. 638]

# 5.15.2 Digitization

Today, the apparently obvious way to implement a (variable) delay is to convert the analog signal to be delayed to a digital value using an *analog-digital-converter*, *ADC* for short. This ADC will typically contain a *sample and hold circuit* to make sure the signal does not change during conversion. The ADC output is connected to a microcontroller which stores the values into successive memory locations of a suitable *random access memory (RAM)*. These values are then read out with suitable address offset and fed to a *digital/analog-converter*, a *DAC*, thereby achieving the desired delay, which is determined by the sampling rate and the address offset. Using off-the-shelf hardware like an Arduino®, such a digital delay can be implemented easily and cheaply. If more than one channel is to be delayed, special precautions must be taken to trigger all input sample and hold circuits in parallel and to employ similar stages following the DACs to avoid data skew.

The main disadvantage of this approach is that time as well as the signal values are necessarily quantized. The time discretization is determined mainly by the speed of the ADCs/DACs, the amount of available memory, and the maximum required delay time *T*. The signal value discretization is determined by the