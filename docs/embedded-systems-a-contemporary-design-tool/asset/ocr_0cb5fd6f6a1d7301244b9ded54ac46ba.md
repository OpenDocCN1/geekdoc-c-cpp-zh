into an ASIC or use in FPGA. Verilog supports the logic gates identified in Figure A.7 as predefined intrinsic modules.

| buf | not |
| --- | --- |
| and | nand |
| or | nor |
| xor | xnor |

Figure A.7 Basic Verilog Logic Gates.

The prototypes for each of the gates are given in Figure A.8.

```
```verilog
buf <name> (OUT1, IN1); // Sets output equal to input
not <name> (OUT1, IN1); // Sets output to opposite of input
and <name> (OUT, IN1, IN2); // Sets output to AND of inputs
or <name> (OUT, IN1, IN2); // Sets output to OR of inputs
nand <name> (OUT, IN1, IN2); // Sets to NAND of inputs
nor <name> (OUT, IN1, IN2); // Sets output to NOR of inputs
xor <name> (OUT, IN1, IN2); // Sets output to XOR of inputs
xnor <name> (OUT, IN1, IN2); // Sets to XNOR of inputs
```
```

Figure A.8 Basic Verilog Logic Gate Prototypes.

The device prototypes appear very much like those for a C or C++ function or procedure. The <name> for a gate instance must begin with a letter and, thereafter, can be any combination of letters, numbers, the underscore _ or the $. Gates with more than two inputs are created by simply including additional inputs in the declaration. Observe that the output list appears first, followed by the input list.

# EXAMPLE A.1

A five-input and gate is declared as

```
```verilog
and <name> (OUT, IN1, IN2, IN3, IN4, IN5); // 5-input AND
```
```

# A.4.1.1 Creating Modules

At the gate level, whether one is building a combinational or sequential logic circuit, a Verilog module really is a collection of logic gates. Each time we declare and define a module, we are creating that set of gates. We will look first at combinational logic models and follow with sequential circuits.

# A.4.1.1.1 COMBINATIONAL LOGIC

The structural or gate-level model of a combinational circuit reflects the physical gates used to implement the design. To illustrate the basic process of creating a Verilog program and modeling combinational logic at the gate level, we will begin with a simple circuit.

An example of a simple module begins with the logic diagram in Figure A.9; the module requires a name, and we will call it AndOr.