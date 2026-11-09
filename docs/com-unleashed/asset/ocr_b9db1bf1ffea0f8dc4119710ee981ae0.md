to those two levels, MTS provides checkpoints at the component level and the interface level. What's more, MTS provides several simple methods for extending security to the method level.

# Making Security Available for a Package and a Component

A role is a group of users. Roles are assigned on a per-package basis. When you create a new package, security is unavailable by default. You can make security available for a package or for a component by performing the following steps.

To make security available for a package, do the following:

+   1. In MTS Explorer, right-click the package and select Properties on the shortcut menu. The Properties dialog box appears.
+   2. On the Security tab, select the Enable Authorization Checking check box and click OK.

To make security available for a component, do the following:

+   1. In MTS Explorer, right-click the component and select Properties on the shortcut menu. The Properties dialog box appears.
+   2. On the Security tab, select the Enable Authorization Checking check box and click OK.

> **Note**
> 
> Security checking is available by default at the component level. In other words, as soon as you make security available at the package level, you must create roles and assign them to each component. Otherwise, every user will be denied permission to the package.

# Creating a Role for a Package

Under DCOM, security is affected programmatically per process. The same is true under MTS: each package is run in a separate process. If you view the Task Manager, you will see that each time a client instantiates a component in a different package, MTS runs a separate instance of Mtx.exe (the surrogate process for the component). Because each package runs in a different process, roles are created in a per-package basis. This is also the reason why a library package cannot use the MTS role-based security. A library package loads in the process space of the caller, and is then bound to the process security