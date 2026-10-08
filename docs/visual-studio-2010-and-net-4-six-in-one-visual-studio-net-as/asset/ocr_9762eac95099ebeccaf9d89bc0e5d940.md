applicable. For other types of object provider environments, some other run-time binding could work. This kind of job is the responsibility of run-time binders. Figure 10-2 shows an architectural overview of how languages, DLR services, and run-time environments work together.

![](bbox=[0.147, 0.196, 0.771, 0.458])

FIGURE 10-2: DLR high-level architecture diagram

The DLR encourages you to interact with dynamic languages and also to create your own dynamic objects. In the remaining discussion of the DLR, you'll learn how easy these tasks are — by going through examples.

# # Invoking IronPython Code Example

In this example, you write a very simple IronPython program and access it with a C# console application. It will be simple, so you should be able to understand it without any Python background. To use IronPython, you must download and install the run-time from the Downloads tab of the IronPython project's home page on CodePlex at `/python/codplex.com`.

Create a C# console application project and name it IronPythonRunner. Use the browse of Add Reference dialog to navigate to the IronPython run-time's installation folder, and add the selected assemblies shown in Figure 10-3 to the project.

![](bbox=[0.563, 0.656, 0.905, 0.866])

FIGURE 10-3: IronPython run-time assemblies