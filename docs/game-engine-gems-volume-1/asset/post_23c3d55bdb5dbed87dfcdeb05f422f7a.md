
definitions, such as metaballs [25], can use the `<extra>` element to store the metaball information and keep a standard mesh geometry to store a generic mesh.

Let's have a look of some design principles that are applied to provide the flexibility necessary to represent data in a common language while still enabling it to be as close as possible to the specific DCC representation as well as enabling internal transformations to move it closer to the engine-specific representation. The remainder of this section is an overview of the COLLADA design principles. For more technically detailed information, the reader can refer to the COLLADA 1.4 and 1.5 specifications available on the Khronos website [22] and on the CD accompanying this book. These specifications and the COLLADA reference book [26] provide more details on the choices made when designing the standard.

## The `<source>` Element

The `<source>` elements contain the raw data that is used by the assets. Like every other element, it has an `id` attribute that has to be unique in a valid document. A source contains a one-dimensional array of data of a specific type (ID, name, boolean, floating-point, or integer). Each element can have a name, which has to be a valid XML string of characters, but the name information is only used to store information relevant for humans and never used to reference an object in a document. Floats and integers can be expressed with any number of digits, providing for any level of accuracy needed. Despite popular belief, there is absolutely no loss of accuracy representing floating point numbers using decimal digits, provided that enough digits are used—9 for single precision and 17 for double precision [27]. The arrays themselves contain a `count` attribute that provides for easier memory allocation.

The `<technique_common>` element provides information about how the source should be accessed by the other elements defined by the specification. The `<technique>` element is where the extensions can be found; an element can carry extensions from several tools at the same time since each tool provides a profile name for its technique.

Figure 2.4 shows that only one array can be in a `<source>` element by using a selector, and it shows that the name attribute is optional (by using dotted lines) and the `id` attribute is mandatory. All this information is stored in the XML schema available on the Khronos website, which can be automatically converted into a drawing or used to validate a document. Listing 2.1 shows what a source looks like in a document and that it is quite easy to parse.

![](img/7ba1225bb0e5a87be0fd35866408ffa7_60_0.png)

### Figure 2.4: Definition of the `<source>` element.

## Listing 2.1: An example `<source>` element and `<accessor>` element.

```
<source id="mesh1-geometry-position">
<float_array id="mesh1-geometry-position-array"
2518.1875 4074.512965 0. 2518.1875 0.
...
</float_array>
<technique_common>
<accessor source="#mesh1-geometry-position-array"
count="8" stride="3">
<param name="X" type="float"/>
<param name="Y" type="float"/>
<param name="Z" type="float"/>
</accessor>
</technique_common>
</source>
```

## The `<accessor>` Element

The `<accessor>` element, shown in Figure 2.5, is where the flexibility is built in. It enables us to organize the arrays in a format that is closer to either the tool or the target format, allowing the build process to convert from one point to another. This provides better decoupling from the exporter's point of view since the exporter can export the data as is and then use the `<accessor>` element to explain how the data should be accessed. The count attribute tells how many elements can be accessed through the `<accessor>` element and what offset and stride is to be used, typically creating n-tuples of data. Then it describes one parameter for each element of the n-tuple, giving it a name and type. An example is shown in Listing 2.1.

![](img/7ba1225bb0e5a87be0fd35866408ffa7_62_0.png)

### Figure 2.5: Definition of the `<accessor>` element.

If a `<param>` element is not given a name, that means the corresponding value is to be ignored. So a source array with 3-tuple values could actually be defining only a 2-tuple with one padding value. As you can see, it is possible within the same language to represent a position array in many different ways. The astute reader will notice that the array element is optional in a `<source>` element, the reason being that an `<accessor>` element can reference an array stored in another `<source>` element, making it possible to reuse the same array of data in a different way through several `<accessor>` elements.

## Geometry and the `<mesh>` Element

Geometry is most often represented by a `<mesh>` element, although the `<convex_mesh>` element and the `<spline>` element are used for rigid body physics and 2D animation curves, respectively. The COLLADA 1.5 specification adds `<brep>` to the list of geometry types. A `<mesh>` element contains a collection of `<lines>`, `<linestrips>`, `<polygons>`, `<polylist>`, `<triangles>`, `<trifans>`, and `<tristrips>` elements. Most likely, the mesh data found right after the export are polygons, and these are transformed into triangles closer to the end of the build pipeline.

A `<mesh>` element contains a mandatory `<vertices>` element, as shown in Figure 2.6. It has one mandatory `<input>` element that references a `<source>` element, meaning it uses the `<accessor>` element in the `<source>` element to access the data. One very interesting design feature is that there is no mention of the dimensionality of the vertex data in COLLADA. In other words, a vertex can have one, two, three, or any number of dimensions, though most content will be using 3D vertices with X, Y, and Z parameter names since transformations and positions are limited to 4D homogeneous coordinate space in the `<scene>` `<node>` element. The `<input>` element associates one semantic with a source. Naturally, the one mandatory input is for the semantic POSITION, which provides the position (e.g., x, xy, xyz, xyzw) of all the vertices used in the mesh primitives. A `<vertices>` element can contain as many `<input>` elements as necessary to attach additional data associated with each vertex. For example, it is customary to have a NORMAL stored per vertex, and it is also common in older systems to have a COLOR per vertex.

![](img/7ba1225bb0e5a87be0fd35866408ffa7_63_0.png)

### Figure 2.6: Definition of the `<vertices>` element.

Referring to the `<triangles>` element in Figure 2.7 as an example of a `<mesh>` element sub-object, one can see it is also composed of a set of `<input>` elements that store the data associated with each primitive as opposed to each vertex as previously done in the `<vertices>` element. One of the `<input>` elements defines the semantic VERTEX, which references by index the POSITION defined in the `<mesh><vertices>` elements used for each primitive. Obviously, there are three vertices per element in a triangle list. The `<p>` element is therefore composed of a PxN set of indexes, where P is the count of primitives and N is the number of `<input>` elements defined in the primitive list.

![](img/7ba1225bb0e5a87be0fd35866408ffa7_64_0.png)

### Figure 2.7: Definition of the `<triangles>` element.

## Conclusion

To conclude this overview of the design of an intermediate asset format and the choices made for the COLLADA standard, it is worth mentioning a few additional high level concepts.

The most important and difficult design concept to keep in mind when designing an intermediate asset format is to try to avoid as much as possible a particular implementation or run-time. In other words, the data should be self-described so it can be transformed and used with any existing or future run-time. This is a really difficult design goal, and it's what occupied most of the design meetings in the COLLADA working group, as the first draft of a feature is always close to how it will be used by the run-time or how it is created in the modeler. Making sure that the data is not described relative to one single usage model is very important, as this ensures the design is not made obsolete as technology is rapidly evolving or is limiting creativity by imposing a model that does not fit with yet-to-be-invented usage models. This one design point is the main difference between COLLADA and most other formats. This difference is obvious when comparing with Autodesk proprietary FBX interchange technology which is defined entirely through an API and specific usage model:

> "The FBX file format is not documented. Applications use FBX SDK to import scene data from an FBX file or to export scene data to an FBX file."
> — FBX SDK Programmer's Guide, page 6 [28].

Another important principle of design is the categorization of elements into `<library_xx>` element types that help with the organization of the data as well as enable document contents to be separated by type. Important is the distinction between the data definition and its utilization through instancing. This enables an element to be used many times without having to repeat its definition, which would cause the size of the intermediate and final assets to bloat tremendously. COLLADA enables some of the values of an element to be modified when instanced through the use of `<param>` elements, so it is possible to share most of the element definition and save a lot of space while still enabling
