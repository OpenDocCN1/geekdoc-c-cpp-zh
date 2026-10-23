
**Table 26.1** Implementation of constraints specified in Hotz et al. (2014) (Chapter 6).

| Name | Description |
|---|---|
| gc1 | No constraint needed: apply refinement of allowed subfeature type<br>`feature MBDiamond subfeature refinement`<br>`CPU allowed features CPUD` |
| gc2 | No constraint needed: apply refinement of allowed subfeature type<br>`feature MBSilver subfeature refinement`<br>`CPU allowed features CPUS` |
| gc3 | In OSAIpha: constraint gc3<br>`every $cpu in $config.Motherboard.CPU`<br>`satisfies $cpu individual of CPUD` |
| prc1&2 | Implemented as a price list, total price is displayed |
| resc1 | Not implemented: the user sees the current price all the time |
| resc2 | The consumed, produced, and free hard disk space are computed with the calculation mechanism: results are shown in the status bar |
| crc1 | In PC, (see Figure 26.3): constraint crc1<br>`((usage = "internet") or (usage = "multimedia"))`<br>`implies present (InternetConn)` |
| crc2 | In PC: constraint crc2<br>`(usage = "scientific") implies (every $cpu in Motherboard.CPU satisfies $cpu individual of CPUD)` |
| crc3 | In PC: constraint crc3 efficiency = Motherboard.efficiency |
| crc4 | In Screen: constraint crc4 efficiency = $config.efficiency |
| compc1 | Implemented as a price list, see Section 26.3 |
| compc2 | Implemented as a price list, see Section 26.3 |
| compc3 | Implemented as a price list, see Section 26.3 |

```
```xml
<configurationPriceList currency="euro" model="ElsieverPC"
    name="euroPricesIncludeTax" tax="0.23">
  <feature name="Screen">
    <attribute name="efficiency">
      <price value="A">200</price>
      <price value="B">150</price>
      <price value="C">100</price>
    </attribute>
  </feature>

  <feature name="CPUD">
    <price>150</price>
  </feature>
</configurationPriceList>
```
```

## 26.4 User Interface Modeling and Generation

### 26.4.1 Layouts

A web-based user interface for the end user is generated without programming. The user makes selections on an HTML form; for example, see the right side of Figure 26.4. The general idea is that each selectable attribute or subfeature of a feature individual being configured generates a question. The modeler creates a layout to define how questions related to a feature individual are divided into pages, the order of questions, and, optionally, the type of input control used for a question.

For example, PC is divided into Requirements (usage, efficiency), software (Operating_System, Applications, storage (for HDUnits)), hardware (Motherboard, Screens), and Internet (InternetConn). These groups are reflected in the configuration tree on the left-hand side of Figure 26.4.

### 26.4.2 Resources

In principle, the language of a configuration model is independent of the language(s) of the end-user interface. A resource file defines display names of objects of the configuration model to be shown to end users and their optional descriptions. In addition, resources define links to web pages providing additional information, messages for broken constraints, and so on. Multiple resources support multiple languages for end users.

Here, few resources were defined, so the names visible to the user come directly from those used in the configuration model (underscores in identifiers were automatically replaced with spaces). For the sake of demonstration, MedStoreDisk was renamed with resources and a descriptive text added to both hard disk types. See the right-hand side of Figure 26.4.

Because the configuration model was created with suitable terminology, near-automatic user interface generation in the primary language was possible.

### 26.4.3 Other User Interface Aspects

The general appearance of the user interface is defined by web-page templates. Defaults were used, except that hard-disk calculation results were added to the status area (upper left-hand side of Figure 26.4). This separates definition of visual appearance from the product-dependent parts of the user interface.

## 26.5 Conclusion

This chapter showed how to model the example PC with VariSales. Taxonomic hierarchy and attributes with refinement, compositional structure, and constraints were applied in a straightforward manner. All aspects were not modeled: Topological (connection) constraints were not modeled because VariSales currently does not support them, and they provide no additional value in the example. Resource constraints were managed through the price and calculation mechanisms. VariSales was built to manage finite configurations. Therefore, the maximum number of Applications is limited, the upper bound is defined with a constant Max_Applications = 20, applied in the subfeature definition Applications.

In future work, direct support for compiling resource constraints into weight constraints rules should be added to efficiently and more proactively support the user in cases that are comparable to the example. The idea of this compilation was described in Soininen et al. (2001).

As a whole, the modeling proceeded smoothly and was able to capture the most relevant aspects. The user interface was semiautomatically generated. In our view, VariSales quite elegantly combines high-level configuration modeling, underlying reasoning, and semiautomatic generation of the user interface.

## Acknowledgments

This work has been supported by Technology Development Centre of Finland and Aalto Service Factory. Basics of VariSales were described in this chapter on the basis of Tiihonen et al. (2013).

## References

- Hotz, L., Felfernig, A., Stumptner, M., Ryabokon, A., Bagley, C., Wolter, K., 2014. Configuration knowledge representation & reasoning. In: Felfernig, A., Hotz, L., Bagley, C., Tiihonen, J. (Eds.), Knowledge-based Configuration – From Research to Business Cases. Morgan Kaufmann Publishers, Waltham, MA, pp. 41–72 (Chapter 6).
- Simons, P., Niemelä, I., Soininen, T., 2002. Extending and implementing the stable model semantics. Artificial Intelligence 138 (1–2), 181–234.
- Soininen, T., Tiihonen, J., Männistö, T., Sulonen, R., 1998. Towards a general ontology of configuration. Artificial Intelligence for Engineering Design, Analysis and Manufacturing (AI EDAM) 12 (4), 357–372.
- Soininen, T., Niemelä, I., Tiihonen, J., Sulonen, R., 2001. Representing configuration knowledge with weight constraint rules. In: Provetti, A., Son, T.C. (Eds.), 1st International Workshop on Answer Set Programming: Towards Efficient and Scalable Knowledge (AAAI Technical Report SS-01-01), pp. 195–201.
- Tiihonen, J., Soininen, T., Niemelä, I., Sulonen, R., 2003. A practical tool for mass-customising configurable products. In: Proceedings of the 14th International Conference on Engineering Design, Stockholm, Sweden, August 19–21, 2003, CDROM, p. 10 (Paper number: 1290).
- Tiihonen, J., Heiskala, M., Anderson, A., Soininen, T., 2013. WeCoTin – a practical logic-based sales configurator. AI Communications 26 (1), 99–131.

## Product Configuration in SAP: A Retrospective

Abstract: This chapter gives a retrospective of the development of the SAP Variant Configurator and the concepts it is based on. The SAP OS/2 configurator that preceded it and the IPC configurator that followed it share this legacy and are also covered. As these three configurators all have their roots in expert systems development projects of the 1980s, the beliefs and motivation of that time are reviewed.

## 27.1 Introduction

The SAP Variant Configurator (SAP VC) is a prominent example of a commercially relevant configurator. It is part of the SAP ERP (Enterprise Resource Planning) systems since R/3 3.0 and thus available to all customers as part of the SAP ERP license. Based on analysis of consulting requests/problem reports and other available data it seems that around 2000 companies employ it, making it one the most used commercial configurators since its inception around 20 years ago. For many companies their business depends on it.

There exists a dedicated book, Variant Configuration with SAP (Blumöhr et al., 2012), which delineates not only the features and business integration of the SAP VC, but also looks at the surrounding ecosystem and customer case studies, and has a brief look at other related SAP configurators. This chapter is not a condensed version of that material, but a retrospective of the development of the SAP VC and the principles from which it is derived. It also uses the development of the configurators at SAP as an example for the commercial side of the evolution of configuration technology, because publications about this are sparse. This retrospective is based on personal involvement both with SAP (since 1992), and before that on participation in the TEX-K and TEX-B expert systems projects mentioned later (for the Battelle Institute, Frankfurt, Germany).

The retrospective covers a succession of three SAP product configurators. The first was a PROLOG based sales configurator with very direct roots in expert systems. It was called the SAP configurator at the time, being the only one. As it was deployed on the OS/2 platform it was also informally referred to as the SAP OS/2 configurator, a designation used here, although not officially correct. The next configurator is the SAP VC, already mentioned (see also Höfling, 2014¹). The third SAP configurator is what is now known as the IPC configurator. Each configurator is based on its predecessor. Many of the
