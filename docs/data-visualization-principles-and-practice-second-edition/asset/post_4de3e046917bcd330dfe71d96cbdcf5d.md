
graphics libraries and the Numerical Algorithms Group (NAG) numerical libraries. IRIS Explorer is particularly attractive for users who wish to combine numerical simulation code with visualization facilities.

**Utilization:** IRIS Explorer provides a visual application builder based on a dataflow application architecture, much like AVS/Express. Modules can be developed in C, C++, and FORTRAN, but also in a proprietary scripting language called SHAPE, which offers an easier way to manipulate complex n-dimensional datasets. Modules are next visually assembled in so-called maps, which are essentially dataflow networks.

## SCIRun

- Type: Application framework
- Availability: Open source
- Address: http://software.sci.utah.edu/scirun.html
- Description: SCIRun is an application framework developed for the creation of scientific visualization applications. SCIRun is very similar in aim and scope to AVS/Express. It provides a set of modules for scientific data visualization that can be connected into so-called networks, following a dataflow application architecture. SCIRun has been used to construct visualization applications for several domains such as finite element numerical simulations, (bio)medical imaging, and computational steering.

**Utilization:** Similar to AVS/Express, SCIRun allows applications to be constructed visually, by editing the dataflow network, or programmatically. Once constructed, applications can be packaged into so-called PowerApps. These are dataflow networks provided with custom user interfaces into turnkey applications that facilitate specific exploration scenarios. Several such PowerApps are available for different domains, such as segmentation (Seg3D), tensor visualization (BioTensor), volume visualization (BioImage), and finite element problems (BioFEM). All in all, SCIRun is a mature environment that covers most needs and requirements of the users of a scientific visualization framework.

## ParaView

- Type: Turnkey system/application framework
- Availability: Open source
- Address: http://www.paraview.org/
- Description: The ParaView system can be used as an end-user tool for visualizing scientific datasets. The main operations for data filtering, selection, mapping, and rendering are provided, such as slicing, isosurfaces, streamlines, and interactive viewing. ParaView provides an intuitive and simple graphical user interface that allows one to both prototype a visualization application and set its various parameters interactively. ParaView is built on top of the VTK class library. The user interface layer is written in the Tcl/Tk scripted languages. Most of the illustrations used in this book were created using ParaView, unless otherwise specified in the text.

**Utilization:** ParaView operates mainly as an end-user system. The application design freedom is considerably less involved, but also easier to learn, than AVS/Express, for example. ParaView makes an excellent system for learning the basics of scientific visualization without having to be a programmer. Only the core VTK functionality is exposed in the user interface. However, developers can add new modules to the ParaView user interface using a mix of Tcl, C++, and XML wrappers.

## MayaVi

- Type: Turnkey system/application framework
- Availability: Open source
- Address: http://mayavi.sourceforge.net/

**Description:** The MayaVi system is an end-user tool for visualizing scientific datasets. Its architecture, provided functionality, and intended user group are very similar to ParaView's. MayaVi is also built as an interactive front-end on top of the VTK class library. However, in contrast to ParaView, MayaVi uses Python as a scripted (interpreted) language to bind user interface functions to the compiled C++ libraries.

**Utilization:** MayaVi operates mainly as an end-user system, similar to ParaView. The user interface is structured differently. A relatively greater emphasis is put on executing operations by writing Python commands at a user prompt than via the user interface itself. The user interface exposes much of the VTK implementation details and is relatively lower-level than the one of ParaView. Overall, although MayaVi and ParaView are quite similar in intention, we find ParaView easier to learn and use and more mature than MayaVi.

## A.3 Imaging Software

In this section, we list a number of imaging software systems. By “imaging,” we refer to several functionalities related to the manipulation and visualization of 2D and 3D image datasets. Such datasets occur frequently in medical practice as the output of the various scanning technologies, such as computed tomography (CT) and magnetic resonance imaging (MRI). Image datasets can contain scalar, vector, and tensor data. Imaging operations cover a wide range of tasks, such as basic data handling and manipulation, basic image processing, image segmentation and registration, shape recognition, image visualization, and volume rendering. Just as for the other types of software systems listed in this appendix, it is not possible to cover all aspects and variants of such systems, so we limit ourselves to a small selection of representative systems.

## The Insight Toolkit (ITK)

- Type: Class library (written in C++)
- Availability: Open source
- Address: http://www.itk.org/
- Description: ITK is a set of class libraries written in C++. The main functionality targeted by the ITK toolkit is divided into three categories: image processing, segmentation, and registration. As such, ITK does not provide visualization (rendering) and user interface facilities. However, ITK can be combined with other toolkits, such as VTK, in order to construct complete visualization applications.

**Utilization:** The software structure of ITK bears a number of similarities to VTK, which is not surprising given the fact that a large number of common organizations and people have been jointly involved in the development of both toolkits. ITK comes with a considerable amount of documentation in the form of books, courses, online material, examples, and demos. Also, the source code of several medical imaging applications built on top of ITK is available for downloading from the ITK site. However, just as for its older cousin VTK, using ITK to construct an imaging application requires a nonnegligible amount of effort, given the sheer size and complexity of the toolkit APIs.

## 3D Slicer

- Type: Turnkey system/application framework
- Availability: Open source
- Address: http://www.slicer.org/
- Description: 3D Slicer is a freely available, open-source application framework for visualization, registration, segmentation, and quantification of medical data. 3D Slicer supports a wide array of tasks, ranging from the investigation and segmentation of volumetric CT and MRI datasets to providing the basic mechanisms for more complex applications, such as guiding biopsies and craniotomies in the operating room and diagnostic visualizations. 3D Slicer can handle scalar, vector, and tensor data attributes. In particular, several functions for visualizing diffusion tensor images, such as principal component analysis, tensor color coding, tensor glyphs, and hyperstreamlines are supported. 3D Slicer is supported by a large number of organizations, and is used in a large number of research projects, as well as in clinical studies and actual applications in the medical practice. Several images created with the 3D Slicer tool are shown in Section 7.6.

**Utilization:** 3D Slicer has an architecture consisting of an end-user front end and a framework that manages a set of application libraries. The front end provides user interfaces and direct mouse-based manipulation of the data, such as picking, probing, and interactive streamline seed placement. The application framework allows one to add new plug-ins in order to provide custom-developed functionality. The 3D Slicer architecture was designed to facilitate adding a wide variety of plug-ins, ranging from standalone binaries (executables and shared libraries) to modules based on the VTK and ITK toolkits and even shell, Tcl, and Python scripts. Although this makes learning the software architecture of 3D Slicer more complex than that of other toolkits such as VTK or ITK, it also makes 3D Slicer more flexible in interfacing with a broad spectrum of third-party software components.

## Teem

- Type: Turnkey/library
- Availability: Open source (written in C)
- Address: http://teem.sourceforge.net/

Description: Teem is a set of coordinated libraries representing, processing, and visualizing scientific raster data. Teem provides functions that support a wide range of operations on n-dimensional raster data (uniform grids) of n-dimensional attributes. The functions of Teem are provided as a set of standalone executables designed much like UNIX filters, which are parameterized by command-line options. The generic data model of Teem, together with the modular decomposition of operations in terms of several filters, allows many complex operations on image volumes to be specified easily and compactly. The set of basic operations provided by Teem include convolution, slicing, resampling, interpolation, statistics, principal component analysis for tensors, color mapping, volume rendering, and tensor glyph visualizations. Several images created using the Teem software are shown in Section 7.5.
