# **FIGURE 21.9** Adding a remote Git repository

![](bbox=[0.282, 0.17, 0.863, 0.489])

To add a repository, click the Add (+) button and choose Add Repository from the menu. A sheet (**Figure 21.9**) will appear, asking you for a name, location, and type. The name is just a convenient identifier and can be anything you like (for example, *My Company Repository* or just *Fred*). The location, however, must be a valid URL to a repository.

The type will be automatically detected when using URLs with schemes like *svn://* and *git://*, but those starting with *ssh://*, *http://*, or *https://* will require you to choose the correct SCM system type in the Type field. The indicator light beneath the Location field will glow green when the supplied URL points to a valid repository.

> **TIP:** The Add a Repository sheet is probably more useful for Subversion repositories, since a cloned Git repository is a copy of the entire repository. For Git, it’s actually more user friendly to add a repository by opening the project in which it’s contained—Xcode will set up everything (including the origin, if one exists) for you.