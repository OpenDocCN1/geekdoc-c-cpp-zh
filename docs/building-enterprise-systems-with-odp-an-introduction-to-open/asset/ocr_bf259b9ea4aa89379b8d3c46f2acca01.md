![](bbox=[0.07, 0.07, 0.9, 0.78])

FIGURE 4.7: Refining the architecture by showing the operation interface signatures for the computational interfaces.

explicit at this level the internal classes that provide the core logic of some of the components and the main data types that they use.

The structure and contents of the data types representing the information managed by the computational objects are specified in the DataTypes package, which is shown in figure 4.8. These data types are derived from the corresponding information object types (which in turn came from the enterprise artefacts, roles and objects). However, this is not simply a matter of copying the model elements concerned. The types do not need to be exactly the same as in the other viewpoints, since refinement or abstraction may be involved. For instance, some additional information has been added in this viewpoint to store usernames and passwords of customers and other stakeholders. Identifiers have also been added to simplify object reference.

Just as in other viewpoints, computational objects introduced in the early stages of the design can later be rewritten as smaller computational objects (by refinement or decomposition), or combined with other computational objects to form a larger computational object (composition). These mechanisms allow