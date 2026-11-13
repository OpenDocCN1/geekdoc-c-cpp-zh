can be exported to both voxel, point cloud, and mesh representations. Support is also included for processing time-dependent volumes, which allow coding various physical simulations that require volumetric domain representations.

Utilization: The main operation mode of OpenVDB is similar to VTK (described above): Users write the intended volume processing scenario as in a C++ program that calls the required functionality provided by OpenVDB classes. Results can be visualized by a number of viewer components provided in OpenVDB itself, or exported to various point cloud file formats. Similar to VTK, this offers a large freedom in building specialized scenarios, but also requires a non-trivial learning curve. While the current focus of OpenVDB is to provide the lower-lever infrastructure required to build end-user applications for volume processing with a focus on volumetric simulations, and less so for interactive volume visualization and exploration, the evolution of OpenVDB will arguably make it easier to use for more general volume processing and volume visualization tasks.

# A.4 Grid Processing Software

In this section, we overview several software systems that address the general task of processing grids. Under the grid denomination, we include all discrete representations of spatial domains which are formed by vertices connected by various cell types. Following the domain modeling terminology introduced in Chapter 3, we consider here software tools that process discrete representations of 2D curved surfaces (mesh processing tools), unorganized point sets, and uniformly sampled 3D volumes (voxel processing tools). Given the wide variety of such tools, the focus is here on tools which implement a comprehensive set of typical operations present in grid processing such as resampling, reconstruction, and filtering, rather than on more specialized tools that focus on a narrower set of operations and/or grid types.

# MeshLab

+   Type: Turnkey system
+   
+   Availability: Open source (written in C and C++)
+   
+   Address: http://meshlab.sourceforge.net/
+   
+   Description: MeshLab is a general-purpose turnkey system for the analysis, processing, and visualization of 3D polygonal meshes. Data can be imported from mesh files in a variety of formats (such as Stanford (PLY), 3D