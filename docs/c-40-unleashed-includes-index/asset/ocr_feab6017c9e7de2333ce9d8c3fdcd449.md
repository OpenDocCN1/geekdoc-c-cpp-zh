# CHAPTER 25

# Assemblies and
Application Domains

# IN THIS CHAPTER

+   - Assemblies 1233
+   - Application Domains 1277

After covering namespaces in the previous chapter, this chapter covers assemblies in detail. We take a look at various types of assemblies you can build from Visual Studio and cover the various settings associated with them. In terms of deployment, we study naming and versioning, as well as the concept of strong names. This provides a segue into the world of the Global Assembly Cache (GAC) for centralized storage of assemblies and the native image generation (NGEN) technology to create native images for intermediate language (IL)-based assemblies. Finally, you’ll see that assemblies are more than containers for IL code and can also contain resources and so on.

To wrap up the chapter, we change our focus from the deployment aspect of assemblies to runtime aspects. You’ll see how assemblies get loaded and how the common language runtime (CLR) establishes isolation using application domains. We also briefly cover .NET Remoting, a low-level communication mechanism between application domains.

# Assemblies

Assemblies are self-describing units of functionality, consisting of code and metadata defining types and their members. Figure 24.3 in Chapter 24, “Namespaces,” illustrates what makes up an assembly. In this part of the chapter, we focus on a set of aspects associated with assemblies, ranging from build time to runtime. While exploring assemblies, we discuss their naming and versioning, the concept of strong naming and the Global Assembly Cache (GAC), how they get loaded, visibility aspects, and more.