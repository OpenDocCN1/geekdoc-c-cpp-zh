# 9.5.2  A Defined Process for PBD

The UDP contains PBD as a special case. This means that we can resolve the issues with PBD by first analysing and designing a problem. We now give some useful guidelines:

+   1. Find host class and policies. Our starting point is to create the system context diagram. In general, the host class corresponds to the SUD system while policies correspond to the SUD’s satellite systems.
+   
+   2. Does each system in the context diagram satisfy SRP? Is there overlap in responsibilities between the systems? Determine how to remedy these problems, for example by ensuring that each system processes its own kind of data or by decomposing it into dedicated systems using the *Whole–Part design pattern* (POSA, 1996). This becomes easier if you can determine which domain category your application is an instance of because the systems have orthogonal responsibilities in those cases.
+   
+   3. Determine the *provides–requires* interfaces of each system in the context diagram. Referring to Figure 9.4 we can say that systems S1, S2 and S3 provide services to the SUD while the SUD provides services to systems S4 and S5 (it is also possible that S4 and S5 require services from the SUD). In some cases system S5 could provide services to the SUD, for example the downloading of reference data that is needed by the SUD.
+   
+   4. Decide how you will design the system as a prototype in C++. Review the prototype and determine if it satisfies the requirements. Asking these questions will hopefully help you to design stable software systems.

# 9.6  USING POLICY-BASED DESIGN FOR THE DVM PROBLEM

We now discuss how to create a simple prototype in C++ for the problem that we introduced in Section 9.3.2. It is easy to create the initial context diagram in Figure 9.3 because the DVM is a special case of an ACS whose context diagram is known. From a project management perspective we have hopefully removed a major source of risk because we have created a stable design that we can extend to satisfy current and emerging requirements.

We choose to implement the system in Figure 9.3 using C++ templates as follows:

```
```cpp
// Notation: GSys == Generic system, not instantiated
template <typename GSource, typename GAuth, typename GResource,
          typename GSink, typename GMIS>

class DVM : private GSource, private GAuth, private GResource,
private GSink, private GMIS
{ // System under discussion
private:

    // C++ does not support interfaces NOR concepts (constraints)
    using GSource::message;

    using GAuth::amount;
    using GAuth::increment;
    using GAuth::decrement;
```

```