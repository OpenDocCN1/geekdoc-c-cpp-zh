
and visualization. Similarly to MeshLab (described above), PCL contains a large set of recent researcher-grade algorithms, which makes it a valuable resource for the researcher or practitioner interested in testing and/or comparing such algorithms. PCL is designed with scalability in mind, and most of its components can efficiently process point clouds of millions of data points.

Utilization: PCL is a class library, which implies that its users need to program their applications using the provided APIs. Although these are very flexible, learning PCL has a steep curve. The extensive use of non-trivial C++ features and design patterns, and its design that relies on fine-grained components, makes it suitable only for the versed C++ programmer, much like, for example, the Boost C++ library. As its documentation uses a relatively more mathematical presentation angle than typical class libraries, PCL developers should be at least familiar with the main computational geometry concepts and terminology.

### CGAL

- Type: Class library
- Availability: Open source (written in C++)
- Address: http://www.cgal.org
- Description: CGAL (the Computational Geometry Algorithms Library) is a class library that includes a wide set of algorithms dedicated to the processing of point clouds and polygonal and volumetric meshes. In contrast to MeshLab, for example, CGAL focuses on providing lower-level functionality, or building blocks, that can be used in the development of applications that need to process grids. Included components cover virtually all well-known computational geometry algorithms, ranging from simple spatial searches and intersection computations, Delaunay and Voronoi diagram construction in 2D and 3D, alpha shapes, surface reconstruction, up to complex polygon and polyhedral decompositions, mesh refinement, and surface parameterization. The design of the library makes extensive use of advanced C++ features such as templates and traits. This makes it possible to parameterize the provided algorithms in a variety of directions, such as choosing the space to work in, interpolation type, or numerical approximations to use. CGAL comes with high-quality documentation and an extensive example set, and is actively maintained and used by a sizeable community. As such, it is arguably the tool of choice for application developers requiring non-trivial computational geometry functionality.
- Utilization: The main operation mode of PCL is similar to VTK (described above): Users write the intended point cloud processing scenario as a C++ program that calls the required functionality provided by PCL classes. Results can be visualized by a number of viewer components provided in PCL itself, or exported to various point cloud file formats. Similar to VTK, this offers a large freedom in customizing specialized scenarios, but also requires a non-trivial learning curve.

## A.5 Information Visualization Software

Compared to scientific visualization systems, information visualization systems come in a larger variety. There are fewer “generic” systems in this category that can be compared to frameworks such as AVS/Express, SCIRun, or IRIS Explorer. One reason is arguably the higher diversity of the application domains, data types, and end user groups for information visualization systems. Consequently, the selection of information-visualization systems presented next has even fewer pretensions to be exhaustive than our selection of scientific-visualization systems. The considered domains for this selection are graphs and trees, multivariate data, and table data.

### The Infovis Toolkit (IVTK)

- Type: Class library/application framework
- Availability: Open source (written in Java)
- Address: http://ivtk.sourceforge.net/
- Description: IVTK is a general-purpose toolkit for developing information-visualization end-user applications and components. IVTK comes as a set of Java class libraries implementing a number of core infovis methods, such as scatter plots, time series, parallel coordinates, matrix plots, and several types of graph and tree layouts.
- Utilization: Developing applications with IVTK and VTK is quite similar. Both are class libraries, so building an application requires programmatically combining instances of the necessary datasets and visualization algorithms. One of the features of IVTK is that it uses a generic dataset model. All datasets (including relational ones) are represented as tables. IVTK provides efficient representations for these tables both in terms of memory and access time. However, just as for VTK, constructing a full-fledged end-user application with IVTK requires a fair amount of work and understanding of the toolkit design. Moreover, compared to VTK, IVTK is relatively newer and less developed toolkit, which provides only a small number of basic versions of the many infovis algorithms that exist for the supported data types (e.g., tree and graph layouts).

### Prefuse

- Type: Class library/application framework
- Availability: Open source (written in Java)
- Address: http://prefuse.org/
- Description: Prefuse is a toolkit for constructing information-visualization applications, and is quite similar to IVTK. The toolkit comes as a set of Java class libraries that provides support for representing the main types of datasets used in information visualization, such as trees, graphs, and tables. Together with these, a number of fundamental algorithms for constructing infovis applications are provided, such as graph and tree layouts, glyphs, dynamic queries, brushing, search, database connectivity, and animation.
- Utilization: Prefuse is both a class library and an application framework. Functionality and data representation are provided in terms of classes. Programming interaction, correlation between multiple views, and application execution is provided by means of framework services. In this respect, prefuse is similar to the VTK and IVTK toolkits. However, the architectures and internals of the two toolkits are quite different. A VTK application is structured like a dataflow pipeline. In prefuse, the accent is laid more on connecting data and processing items via actions and events. All in all, prefuse is a good start to start experimenting with information-visualization concepts and algorithms via prototyping. However, the toolkit does not yet have a wide palette of implemented algorithms, which is similar to IVTK. Also, the scalability and efficiency of the implemented algorithms cannot yet cope with truly large datasets.

### GraphViz

- Type: Library and turnkey system
- Availability: Open source (written in C)
- Address: http://www.graphviz.org/
- Description: GraphViz is a high-quality library for computing and displaying graph layouts. GraphViz implements several popular graph-layout algorithms such as rooted and radial trees, hierarchical directed acyclic graph layouts, and force-directed layouts. In addition to layout, GraphViz offers advanced control of the mapping and rendering of graph nodes and edges, including annotations, spline edges, and nested graphs. An extensive set of options allows one to specify the finest details of the layout and mapping. Its robustness, scalability, simplicity of use, and availability have made GraphViz one of the best-known toolkits for laying out graphs and quickly producing quality graph visualizations. Several graph visualizations created with the GraphViz software are shown in Section 11.4.2.
- Utilization: GraphViz is structured as a set of separate executables. These read and write graph specification files in various formats. These executables can be easily used as turnkey systems to load, lay out, and draw graphs. In addition to these, GraphViz also provides an API that allows more flexible access to the layout functionalities. This allows one to use GraphViz as a layout library on behalf of other applications.

### Tulip

- Type: Library and turnkey system
- Availability: Open source (written in Java)
- Address: http://www.tulip-software.org/
- Description: Tulip is a framework for the manipulation and visualization of large graphs. At the core of the Tulip system is an efficient data representation that allows manipulation of graphs with more than one million elements. The Tulip framework contains a core library and an end-user visualization tool. The library provides graph data representation and so-called algorithms. The algorithms include several layout engines (rooted, radial and bubble trees, treemaps, and force-directed) and rendering engines that allow one to parameterize the node and edge glyphs by graph data attributes. Apart from these, several graph data manipulation algorithms are provided, such as editing, clustering, decomposition, and computing statistics on graphs. Several tree visualizations created with the Tulip system are shown in Section 11.4.1.
- Utilization: Tulip can be used either as a C++ class library or as a turnkey system. In the first case, developers build their application on top of the core Tulip graph data and algorithm classes. In the second case, end users can use the Tulip visualization front-end to interactively import, navigate, edit, lay out, and render graphs in a variety of ways. The functionality of the Tulip front-end, although not covering all the functions of the core library, is rich and customizable enough to allow one to use this application as a full-fledged viewer for complex graphs in real applications. Similar to ParaView and MayaVi, the Tulip front-end can be customized via a plug-in mechanism to load additional functionality developed on top of the core libraries.

### Gephi

- Type: Library and turnkey system
- Availability: Open source (written in C++)
