# 26.2.2 Compositional Structure

A feature type defines its compositional structure through a set of subfeature definitions. A subfeature definition specifies a subfeature name, a nonempty set of possible subfeature types (allowed types for brevity), and a cardinality indicating the valid number of subfeatures.

In a configuration, subfeatures (parts) of a feature individual are realized with feature individuals. The realizing feature individual(s) “fill the role” created by the effective subfeature definition. An explicit empty realization is possible, when cardinality 0 is allowed. An “optional part” common in industrial products is modeled as a subfeature that allows an empty realization. A default realization can include attribute values and subfeature realizations of arbitrary depth. In addition, an empty realization (special value none) can be set as the default realization. Inherited subfeatures can be refined by restricting allowed types, cardinality, or by modifying or hiding default subfeature realizations.

The compositional structure is shown in the subfeature hierarchy tree (lower left-hand side of Figures 26.1 and 26.2). Drag & Drop from the feature type tree enables adding allowed feature types, subfeature definitions, and defaults.

The right-hand side of Figure 26.2 shows an overview of subfeatures of the feature type HDUnit. Each HDUnit has as part named HD_Controllers 1 to 2 individuals of any subtype of HDController, and as Hard_disks 1 to 4 individuals of any subtype of HDisk. No defaults are set for the subfeatures.

In the textual PCML presentation the corresponding part of the configuration model is expressed as follows:

```
feature HDUnit
  subtype of PC_Component
```

![](bbox=[0.12, 0.512, 0.845, 0.77])

# FIGURE 26.2

Compositional structure of HDUnit in VariSales Modeling Tool.