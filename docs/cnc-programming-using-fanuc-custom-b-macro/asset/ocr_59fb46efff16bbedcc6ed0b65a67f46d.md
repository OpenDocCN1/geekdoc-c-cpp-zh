Note that the parameter values that are most suitable for most of the cases are already set by the MTB. Any change in these values is not recommended because an incorrect setting may result in unpredictable, possibly dangerous, behavior of the machine, causing injury to the operator or damage to the machine or both. However, certain parameters, such as those for software overtravel limits, G-code system selection (A, B, or C) on a lathe, straight-line positioning with G00, calculator-type data entry (so that X10, e.g., is interpreted as 10 mm, not as 10 μm), etc., may need to be changed to suit a particular application. However, in such cases, first note down the original settings before making any change, so that one may revert back to the original values, in case of any incorrect setting. Any change must be done by an experienced person, after thoroughly studying the parameter which is intended to be changed. The complete description of all the parameters can be found in the *Parameter Manual* supplied with the machine.

Further discussion necessitates a clear understanding of types of parameters. There are, broadly speaking, four types of parameters: *bit type* (permissible data 0 or 1), *byte type* (permissible data range −128 to 127, or 0 to 255), *word type* (permissible data range −32,768 to 32,767, or 0 to 65,535) and *two-word type* (permissible data range −99,999,999 to 99,999,999). The bit-type parameters have rows of eight bits (bit #0 at the extreme right and bit #7 at the extreme left). Some bit-type parameters have multiple rows of eight bits in each row, corresponding to each machine axis. Several other parameters also have multiple rows for different axes. On a two-axis lathe, the first row corresponds to the X-axis, and the second row to the Z-axis. On a three-axis milling machine, the three rows correspond to the X-, Y-, and Z-axes, respectively. Such parameters are called axis-type parameters. For the purpose of effective memory utilization, different types of parameters are used for different applications. For example, I/O CHANNEL is a byte-type parameter, whereas the parameters for setting software overtravel limits (distances in microns, machine coordinate system) and two-word parameters.

The format for programmable parameter entry is as follows:

```
G10 L50;       (Parameter entry mode starts)
N_ R_;         (For parameters other than axis-type)
N_ P_ R_;      (For axis-type parameters)
...
...             (Multiple parameter entry is permitted)
...
G11;            (Parameter-entry mode ends)
```

where

L50 selects parameter-entry mode,
N contains parameter number,
P contains axis number (used for axis-type parameters only),
R contains the specified value of the parameter.