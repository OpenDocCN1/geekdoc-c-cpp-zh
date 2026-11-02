refinement route is not always appropriate, but the rewards of doing so are considerable; this is what the model-driven approach is trying to do.

Work to raise the abstraction level at which designs are formulated has been a major research thread for a long time and, as should now be clear, was an important influence on the development of the ODP viewpoints. However, the ideas gained prominence in 2001 when the OMG brought much of the earlier thinking together in their MDA white paper [92]. This focused initially on one particular problem, the decoupling of application designs from the details of the growing number of middleware platforms available. The answer proposed was to capture the application detail in a quite abstract model and then provide tools that could specialize this single design for each of the platforms available.

One of the main contributions was to recast thinking that had previously been in terms of translation between languages with different grammars so that the ideas were expressed as models whose form was governed by corresponding metamodels (although a metamodel is still, basically, just a grammar). If the transformation that was needed from abstract and concrete models could be defined in terms of metamodels, a single tool generated from them could be used for transforming the whole family of models that shared the same metamodel (see figure 15.1). In practice, transformations need to be parameterized to make them more widely applicable, so the process is steered by a combination of the material embedded in the transformation and some additional information supplied when a particular transformation activity is performed.

Later, the OMG extended their architecture to support more than one refinement step, and identified three major modelling levels, yielding

![](bbox=[0.17, 0.626, 0.792, 0.874])

FIGURE 15.1: A framework for model transformations.