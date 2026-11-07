+   - **module name**—The name specified in a module’s module declaration. All module units in a given module must have the same module name.
+   - **module partition**—A module unit in which the module declaration specifies the module name followed by a colon and a partition name. Module partition names in the same named module must be unique. If a module partition is a module interface partition, it must be exported by the module’s primary interface unit.
+   - **module purview**—The set of identifiers within a module unit from the module declaration to the end of the translation unit.
+   - **module unit**—An implementation unit containing a module declaration.
+   - **named module**—All module units with the same module name.
+   - **named module purview**—The purviews of all the module units in the named module.
+   - **namespace**—Defines a scope in which identifiers and variables are placed to help prevent naming conflicts with identifiers in your own programs and libraries.
+   - **partition**—A kind of module unit that defines a portion of a module’s interface or implementation. Partitions are not visible to translation units that import the module.
+   - **precompiled module interface (.pcm)**—A clang++ file that contains information about a module’s interface. Used when compiling other translation units that depend on a given module.
+   - **primary module interface unit**—Determines the set of declarations exported by a module for use in other translation units.
+   - **:private module fragment**—A section in a primary module interface unit that enables you to define a module’s implementation in the same file as its interface without exposing the implementation to other translation units.
+   - **reachable declaration**—A declaration is reachable if you can use it in your code without referencing it directly. For example, if you import a module into a translation unit and one of the module’s exported functions returns an object of a non-exported type, that type is reachable in importing translation units.
+   - **translation unit**—A preprocessed source-code file that is ready to be compiled.
+   - **visible declaration**—A declaration you can use by name in your code. For example, if you import a module into a translation unit, the module’s exported declarations are visible in that translation unit.