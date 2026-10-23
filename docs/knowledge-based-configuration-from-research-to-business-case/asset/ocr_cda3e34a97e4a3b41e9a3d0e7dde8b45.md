Table 25.2 Product properties of working example. For example, each computer configuration has a specified cpu type *pcpu* (*CPUS* or *CPUD*).

| Product Property | Domain |
|---|---|
| pname | Text |
| pcpu | CPUS, CPUD |
| pmb | MBSilver, MBDiamond |
| pos | OSAlpha, OSBeta |
| pprice | Integer |

Table 25.3 Incompatibility constraints of working example. For example, a motherboard *MBSilver* is incompatible with the energy efficiency class *A*.

| Attribute | Property | Attribute | Property |
|---|---|---|---|
| efficiency | A | mb | MBSilver |
| efficiency | C | mb | MBDiamond |

Table 25.4 Filter constraints of working example. For example, the *cpu* selected by the customer has to be included in the corresponding configuration.

| Attribute | Operator | Attribute |
|---|---|---|
| maxprice | ≥ | price |
| cpu | = | pcpu |
| mb | = | pmb |

be *MBDiamond*. The complete list of incompatibility constraints in our working example is shown in Table 25.3.

*Filter Constraints.* In WEEVIS, filter constraints are used for expressing the relationship between selected customer requirements (instantiations of customer properties) and the corresponding product properties. For example, the price of a solution must not exceed the maximum price defined by the user or the selected *cpu* should be contained in the configuration. The complete list of filter constraints used in this working example is shown in Table 25.4.

*Includes.* This is an additional constraint type that allows the definition of *alternative inclusions* that are not taken into account by incompatibility and filter constraints. An example of such an inclusion constraint is the following: if the user is interested in a highly energy-efficient computer, include the