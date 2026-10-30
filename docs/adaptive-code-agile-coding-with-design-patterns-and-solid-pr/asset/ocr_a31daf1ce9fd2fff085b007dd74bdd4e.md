![](bbox=[0.18, 0.04, 0.52, 0.78])

# FIGURE 11-2 The AccountController is still at the mercy of too many implementations.

If you build the Controllers project in isolation, you will still find NHibernate in the bin/ directory, indicating that it is still implicit dependency. Although you have made excellent steps to separate the AccountController class from any unnecessary dependencies, it is still not loosely coupled from the implementations in each dependent assembly.