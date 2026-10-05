FIGURE 6-37 The keyboard class.

To summarize, the order of driver loading for a device is as follows:

+   1. The bus driver is loaded, creating the PDO.

+   2. Any lower filters listed in the Hardware instance key are loaded, in the order listed (multi string), creating their filter device objects (FIDs) in Figure 6-34).

+   3. Any lower filters listed in the corresponding Class key are loaded in the order listed, creating their Fidos.

+   4. The driver list listed in the Service value is loaded, creating the FDO.

+   5. Any upper filters listed in the Hardware instance key are loaded, in the order listed, creating their Fidos.

+   6. Any upper filters listed in the corresponding Class key are loaded in the order listed, creating their Fidos.

To deal with multifunction devices (such as all-in-one printers or cell phones with integrated camera and music player functionalities), Windows also supports a container ID property that can be associated with a devnode. The container ID is a GUID that is unique to a single instance of a physical device and shared between all devnodes that belong to it, as shown in Figure 6-38.

![](bbox=[0.165, 0.598, 0.705, 0.813])

FIGURE 6-38 All-in-one printer with a unique ID as seen by the PnP manager.