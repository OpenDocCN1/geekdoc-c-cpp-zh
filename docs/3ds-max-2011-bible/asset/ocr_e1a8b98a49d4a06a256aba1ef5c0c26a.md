# Primitive Maintenance Modifiers

Included among the Mesh Editing modifiers are two unique modifiers that can be applied to primitive objects, allowing them to maintain their parametric nature.

# Note

Using the Edit Mesh or Edit Poly modifiers increases the file size and memory required to work with the object. You can reduce the overhead by collapsing the modifier stack.

# Edit Mesh modifier

All mesh objects are by default Editable Mesh objects. This modifier enables objects to be modified using the Editable Mesh features while maintaining their basic creation parameters.

When an object is converted to an Editable Mesh, its parametric nature is eliminated. However, if you use the Edit Mesh modifier, you can still retain the same object type and its parametric nature while having access to all the Editable Mesh features. For example, if you create a sphere and apply the Edit Mesh modifier and then extrude several faces, you can still change the radius of the sphere by selecting the Sphere object in the Modifier Stack and changing the Radius value in the Parameters rollout.

If the Sphere base object is selected after a modifier has been applied, the Topology Dependence warning dialog box appears. This dialog box doesn't prevent you from making any changes to the base object parameters, but it reminds you that changes you make to the base object's parameters may disrupt the changes to the surface accomplished by the modifiers. The warning dialog box also includes a Hold button to load the current scene in a buffer in case you don't like the results.

# Caution

One drawback of the Edit Mesh modifier is that its subobjects cannot be animated.

# Edit Poly modifier

The Edit Poly modifier lets you work with primitive objects using the operators found in the Editable Poly rollouts. A huge benefit of this modifier is that you can remove it at any time if the changes don't work out.

The Edit Poly modifier includes two separate modes: Model and Animate. You can select these modes in the Edit Poly Mode rollout, shown in Figure 26.6.

# FIGURE 26.6

The Edit Poly Mode rollout lets you switch between Model and Animate modes.

![](bbox=[0.04, 0.00131, 0.22, 0.00149])

Model mode lets you access the same features available for Editable Poly objects. Animate mode lets you animate subobject changes made with the features used to edit the object. To animate these subobject changes, you use the Auto Key or Set Key buttons to set the keys.