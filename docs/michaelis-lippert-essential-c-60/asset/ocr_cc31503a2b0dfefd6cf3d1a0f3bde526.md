![](bbox=[0.13, 0.1, 0.78, 0.42])

# FIGURE 21.2: Assemblies with the Modules and Files They Reference

Even though an assembly can include multiple modules and files, the entire group of files has only one version number, which is placed in the assembly manifest. Therefore, the smallest versionable component within an application is the assembly, even if that assembly is composed of multiple files. If you change any of the referenced files—even to release a patch—without updating the assembly manifest, you will violate the integrity of the manifest and the entire assembly itself. As a result, assemblies form the logical construct of a component or unit of deployment.

> NOTE
> Assemblies—not the individual modules that compose them—form the smallest unit that can be versioned and installed.

Even though an assembly (the logical construct) could consist of multiple modules, most assemblies contain only one. Furthermore, Microsoft provides an ILMerge.exe utility for combining multiple modules and their manifests into a single file assembly.