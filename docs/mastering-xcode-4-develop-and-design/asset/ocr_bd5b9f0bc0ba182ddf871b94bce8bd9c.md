# WHAT IS A WORKSPACE?

Xcode 4 introduces the idea of a workspace as a kind of project binder—a container for multiple projects. A project groups together its related files and settings; a workspace binds multiple related projects. A workspace merely contains pointers to Xcode projects. Projects remain distinct in that you can remove them from a workspace without affecting the project’s content or settings. In other words, the project can still be opened and edited outside its workspace. Workspaces give you several advantages over projects that reference files and built products from other projects.

Projects contained within the same workspace share a common build location. This makes it possible for one project to use another’s built products. This one feature makes a world of difference for managing complex applications and application suites. It makes it far easier, for example, to include the built product of a common framework project into one or more of your application projects.

The automatic dependency detection you learned about in Chapter 14 extends to the workspace level as well. This means that including a product’s framework in the target of an application project within the same workspace usually requires no additional work for Xcode to recognize the dependency. As with dependent targets within the same project, Xcode will see this dependency and build the framework before building the application. In other words, you don’t have to copy shared libraries into each project folder in which you intend to use the library.

> NOTE: Xcode may not be able to detect complex dependencies automatically. In this case, you’ll need to disable the Find Implicit Dependencies setting of the affected scheme and add and sort the interdependent targets manually.

![](bbox=[0.0, 0.62, 0.25, 0.78])