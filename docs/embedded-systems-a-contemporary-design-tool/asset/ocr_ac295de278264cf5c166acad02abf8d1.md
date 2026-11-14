In the models, the extra delay through the path with the inverter leads to the hazards. The problem cannot be fixed by inserting additional buffers to try to match path lengths. The natural variation in the values of electrical parameters across large part lots makes such an approach ineffective in mass-produced products.

# ## 2.3.3.2 Dynamic Hazard

A dynamic hazard exists when the circuit output may erroneously change more than once as the result of a single input transition. The circuit in Figure 2.18 contains a dynamic hazard.

![](bbox=[0.283, 0.25, 0.703, 0.382])

**Figure 2.18** A Digital Circuit with a Dynamic Hazard

Observe that the path through a portion of the circuit is slow; that is, the propagation delay through the gates is at the high end of the specification. A second path comprises gates that have a delay at the low end of the specification. The remaining devices are assumed to have typical delays (which fall between the short and long delays) and to all be of the same value.

The quiescent conditions on the input signals are specified. We assume that the signals have been stable for a time that is much greater than the propagation delay through the circuit. The signal on input B is then changed from a logical 0 to a logical 1. The diagram illustrates the propagation of that signal though the logic. Observe that the output signal makes three state changes before it finally settles.

The Verilog module in Figure 2.19 models a dynamic hazard.

```
```verilog
// Modeling a Dynamic Hazard
module Dynamic0 (E, term0, term1, term2, A, B, C, D);
    // declare the inputs and outputs
    input   A, B, C, D;
    output  E, term0, term1, term2;
    parameter delay0 = 10;
    parameter delay1 = 5;
    // build logic functions
    not   #delay0 invN(B, B);
    and   #delay0 and0(term0, A, B);
    and   #delay0 and1(term1, nB, C);
    and   #delay0 and2(term2, nB, term1);
    and   #delay1 and3(term3, nB, D);
    or    #delay1 or0(E, term2, term3);
endmodule
```
```

**Figure 2.19** Modeling a Dynamic Hazard