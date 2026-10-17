# BUILD SETTINGS

*Build settings* include the target architecture and SDK, the location of intermediate build files, compiler selection (LLVM versus GCC, for example), linker settings, search paths, and more. The settings can be project-wide or target-specific, and a separate value can be defined for a given configuration (Debug versus Release, for example).

# CONFIGURATIONS

A *configuration* describes a collection of build settings for the build environment. By default, an Xcode project has two configurations: Debug and Release. The configuration Xcode uses when performing a given action (such as Run, Analyze, or Archive) is dictated by the settings in the active scheme. For example, the Run action of the default scheme of a Cocoa application project would use the Debug configuration, while the Archive action would use the Release configuration. Common configurations can be exported and imported to enable sharing and reuse between an organization’s projects.

# RUN DESTINATIONS

A *run destination* describes the environment in which to run an executable product (that is, a target that specifies an application or command-line program). The environment can be your Mac (in 32-bit or 64-bit mode), the iOS Simulator, or an actual iOS device. The available run destinations shown in the Scheme controls are determined automatically by the build settings specified for the associated target—specifically, the combination of settings specified in the Supported Platforms, Architectures, and Base SDK build settings.