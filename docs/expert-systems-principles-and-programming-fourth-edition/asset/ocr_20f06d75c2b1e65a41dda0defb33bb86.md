# # CHAPTER 12
# Expert System Design Examples

# ## 12.1 INTRODUCTION

This chapter provides several examples of CLIPS programs. The first example demonstrates how uncertainty can be represented in CLIPS. The next two examples demonstrate how other knowledge representation paradigms can be emulated using CLIPS. One shows how decision trees can be represented in CLIPS and the other shows how backward-chaining rules can be represented in CLIPS. The fourth and final example builds the framework of a simple expert system that monitors a group of sensors.

# ## 12.2 CERTAINTY FACTORS

CLIPS has no built-in capabilities for handling uncertainty. However, it is possible to incorporate uncertainty into CLIPS by placing information dealing with uncertainty directly into facts and rules. As an example, the MYCIN uncertainty mechanism will be emulated using CLIPS. This section will demonstrate how the following MYCIN rule (Firebaugh 88) can be rewritten in CLIPS:

```
IF
  The stain of the organism is gramneg and
  The morphology of the organism is rod and
  The patient is a compromised host
THEN
  There is suggestive evidence (0.6) that the
  identity of the organism is pseudomonas
```

MYCIN represents factual information as object-attribute-value triples. These OAV triples can be represented in CLIPS using the following deftemplate