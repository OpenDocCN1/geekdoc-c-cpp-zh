Yotta creates a set of folders complete with a json file describing the project:

| Name |
| - source |
| test |
| module.json |

At this point the source and test folders are empty. These are where you are supposed to put your code files for the project and any tests you want to implement.

# Adding a Dependency on the Micro:bit Library

You could start populating the source folder with whatever program you wanted to write, a micro:bit program has a dependency on the micro:bit library which needs to be added. How this done is slightly different from installing a standard mbed dependency.

At the moment the micro:bit library is not hosted by mbed and so you have to download it from its GitHub repository. However, before we can add any dependencies, we have to set the target for the project. In principle, you only have to do once for any yotta session, but in practice you might find that it gets forgotten or overwritten. For the micro:bit you set the target using:
yotta target bbc-microbit-classic-gcc

You will see:

+   - info: get versions for bbc-microbit-classic-gcc
- info: download bbc-microbit-classic-gcc@0.2.3 from the public module registry
- info: get versions for mbed-gcc
- info: download mbed-gcc@0.1.3 from the public module registry

This adds a yotta_targets directory with some files that are needed for the target:

| source |
| test |
| yotta_targets |
| yotta.json |
| module.json |