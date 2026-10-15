# 1

# Introduction

# 1.1 Subdivisions of Geometric Objects

Now, everyone knows several applications for which it is necessary to represent geometric objects in a computer, for instance in the fields of architecture, computer-aided design and manufacturing, geology, medical simulation, image synthesis, video games, medical or biological image processing and analysis, etc.

Representing a geometric object is necessary to compute “information”:

+   - *about* the object, for instance computing geometric properties, extracting images, etc. Often, the object is *analyzed* in some way;
+   - *using* the object, for instance for *simulating* some phenomenon: physical, biological, etc.

So various needs lead to very different methods for representing geometric objects [172, 178, 2]. Among them, many deal with *subdivided* geometric objects.

# 1.1.1 Subdivided Objects

Look at the cube of Fig. 1.1(a). Different parts can be distinguished, according to:

+   - geometric properties. A geometric cube can be associated with this cube of the real world, and it is well-known that a full cube is made by (or *subdivided into*) one *volume*, six *faces*, twelve *edges* and eight *vertices*. Each of these parts is a connected set of geometric points: for instance, a face is a part of the *boundary* of the cube, which contains all coplanar points; each edge is the intersection of two faces. Note that all faces are *incident* to four edges and four vertices: all faces have thus the same *structure*.
+   - color. For instance, the upper face can be itself subdivided into two parts: one corresponds to the letter, the other to the complement of the letter in the upper face of the cube. They are 2-dimensional parts,