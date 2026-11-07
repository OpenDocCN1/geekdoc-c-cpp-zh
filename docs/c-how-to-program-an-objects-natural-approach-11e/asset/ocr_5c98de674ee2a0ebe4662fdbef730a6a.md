# 16.8.3 : private Module Fragment

Modules also support separating interface from implementation in one translation unit by using a `:private` module fragment in the primary module interface unit, as in:<sup>54,55,56</sup>

```
export module name; // introduces the module name
// code that defines the primary module interface
// private module fragment for defining implementation details
module :private;
// implementation details
```

With this approach to defining a module, the primary module interface unit must be the module’s only module unit. Changes to the implementation details in the `:private` module fragment do not affect this module’s interface, nor do they affect other translation units that `import` this module.<sup>57</sup>

Use the `:private` module fragment when you want to manage your interface and implementation details in one translation unit. The `:private` module fragment is essentially a module implementation unit after

```
module :private;
```

but you don’t need to compile a separate `.cpp` file. Another potential benefit is that having all the code in a single interface may enable the compiler to better optimize the code.<sup>58</sup>

# 16.9 Partitions

You can divide a module’s interface and/or its implementation into smaller pieces called partitions. When working on large projects, this can help you organize a module’s components into smaller, more manageable translation units. Breaking a larger module into smaller translation units also can reduce compilation times in large systems—only translation units that have changed and translation units that depend on those changes would need to be recompiled.<sup>59</sup> Whether items are recompiled would be determined by the compiler. The compiler aggregates a module’s partitions into a single named module for import into other translation units.