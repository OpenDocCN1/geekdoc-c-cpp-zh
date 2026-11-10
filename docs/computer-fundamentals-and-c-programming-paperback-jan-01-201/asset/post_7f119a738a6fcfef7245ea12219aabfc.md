
> **Tip:** Choose the lowest resolution that will serve your purpose. Low resolution and black-and-white images have small file sizes. Size is a limiting factor when files are sent across the Internet. The cost of transmission is directly related to the size of the file.

Modern scanners have the *Optical Character Recognition (OCR)* facility by which a document (or its image) can be scanned in a special mode to *extract the text as a stream of characters*. This needs special software that can interpret the dot pattern in a picture as a character, say, A. The advantage in using OCR is that an image file can be converted to a text file which can be edited with text editing software. The file size also reduces substantially. If your existing scanner doesn't have the OCR function, then you need an OCR scanner.

> **Takeaway:** If you have lost the file of a Word document but have its hard copy, then you can use OCR to "restore" the file which can then be edited with the same software.

There are other types of scanners available. Hand-held scanners are manually moved across the document. Banks use *Magnetic Ink Character Recognition (MICR)* scanners to read the codes printed on bank cheques. Shops use hand-held barcode scanners to determine the product name and price from the barcodes printed on the product label.

## 1.13 OUTPUT DEVICES

Do all programs generate output? The vast majority of them do. We generally use the term "output" to mean information that can be seen or heard. Printers and loudspeakers belong to this category. The scanner creates an image of a document but saves the "output" to disk. That, for us, is not output. In the following sections, we will discuss the commonly used visual output devices.

### 1.13.1 The Monitor

The monitor is an integral part of a computer's configuration. Programs use it to display text or graphical output, while users also need a monitor to view the input that they key in. The performance of a monitor is judged mainly by its image quality, resolution, energy consumption and its effect on the eyes. There are two competing technologies; the old CRT monitors have virtually made way for the modern LCD-based types. Monitors are connected to the desktop's VGA or DVI port. The connection is internal for the laptop.

**CRT Monitor** The CRT (cathode ray tube) monitor uses a rarefied tube containing three electron guns (for the three primary colors) and a screen coated with phosphorescent material. The guns emit electrons to create images on the screen by selectively lighting up the phosphors. CRT monitors typically have a resolution of 640 × 480 pixels which translates to an *aspect ratio of 4:3* (Aspect ratio = width / height). They are large and heavy, energy-inefficient and generate a lot of heat.

**LCD Monitors** Most computers today are shipped with LCD monitors (or their variants, LED and TFT). An LCD screen comprises thousands of liquid crystals, which, by themselves, don't generate light but may allow or block the passage of light through them. An image is formed by selectively applying a voltage to these crystals and using a separate light source for light to pass through them. The backlight is provided either by fluorescent light (the standard LCD) or by LEDs (hence the term *LED monitors* and *LED TVs*).

LCD monitors have a wider aspect ratio (16:9) compared to the 4:3 offered by CRT monitors. From a generic standpoint, they have greatly improved upon the drawbacks of the CRT monitor. They consume less power, generate less heat, have increased life span and take up a lot less space. It is even possible to mount an LCD monitor on the wall. However, the viewing angle is less than 180 degrees, but this attribute is undergoing constant improvement.

**Note:** LEDs are simply backlight providers and have no role in the formation of the image. The newer TFT (thin film transistor) is simply a variant of the basic LCD technology.

### 1.13.2 Impact Printers

Printers produce *hard copies* of output (in contrast to disk files which are soft copies) which include text and graphics. There are currently two basic technologies used for printing—impact and non-impact. The older impact technology uses a printhead to strike (impact) a ribbon placed between the printhead and paper. Impact printers are noisy and are being phased out, but one variant (the dot-matrix printer) is still in active use.

**Dot-matrix Printer** The printhead of the dot-matrix printer has either 9 or 24 pins which are fired in multiple combinations to generate letters, numerals and symbols. The ribbon is impregnated with ink, and when the pins fire against the ribbon, an impression is created on the paper behind it. The paper itself is moved forward by a drum after one line of printing has been completed. Because each pin can be controlled individually, it is possible to print graphics with this technology. However, multiple fonts can’t be used.

The speed of a dot-matrix printer can be as high as 300 cps (characters per second). A printer with 24 pins offers the best print quality (low as it is) at 144 dpi (dots per inch). However, the gaps between the pins are clearly visible, so this technology doesn’t produce quality output. This printer type refuses to go away simply because it can produce carbon copies on continuous stationery. Invoices and bills are often printed in multiple copies, the reason why shops generally use dot-matrix printers.

**Daisy-wheel Printer** The now obsolete daisy-wheel printer uses a different technology to strike the ribbon. It employs a wheel with separate characters distributed along its outer edge. The characters are thus pre-formed and not generated. For printing a character, the wheel is rotated so that the desired character directly faces the ribbon. You can’t print graphics with this printer but you can change the wheel to obtain a different set of fonts.

**Line Printer** For heavy printing, the line printer is still the best bet. This technology uses a print chain containing the characters. The chain rotates continuously in front of the paper. Hammers strike the paper in the normal manner, but the print speeds attained with this technology are as high as 1200 lpm (lines per minute). Line printers are used to print low-quality voluminous reports and can print unattended for long stretches of time. However, a line printer is extremely noisy, the reason why it is generally kept in a separate room.

## 1.14 COMPUTERS IN A NETWORK

Most organizations, large or small, no longer have standalone computers. Today, computers cooperate with one another by being connected to a network. An authorized user can now share their files with other users. An application run by multiple users can now be hosted on a single machine instead of being stored on individual machines. Many network applications today are designed in a way that enable sharing of the workload by multiple machines. As rightly perceived by Sun Microsystems many years ago, “the network is the computer.”

Apart from sharing files and programs, a network allows the sharing of scarce hardware resources by all connected computers. A printer can be used by several users if the printer itself is connected to one of the computers in the network. The computer (or *node*, in network parlance) that offers these services would need to be more powerful than the computers it serves. That’s how *servers* came into being as the central nodes in a network. Servers also form the backbone of the largest network of all—the Internet.

All networked nodes need a common addressing scheme that would ensure delivery of data to the right node. The scheme used by most is *Ethernet*, a hardware standard that defines the addressing, cabling and signaling requirements of the network. Ethernet is currently the dominant technology, having replaced the *token ring* and *FDDI* technologies. In this scheme, data are divided into *frames* containing the source and destination addresses. A set of network *protocols* (rules) are also used for data transmission, but they will be discussed in Chapter 2.

> Note: Ethernet, token ring and FDDI are hardware technologies. For a network to function, a set of network (software) protocols also need to run. *TCP/IP* is the most dominant network protocol and it powers the Internet.

### 1.14.1 Network Topology

There are a number of ways or *topologies* of connecting computers (Fig. 1.7), each having its own merits and demerits. The *bus topology* uses a single cable as a bus to which all computers are connected. The failure of a single node doesn’t disrupt the communication between the remaining nodes.

The *star topology* uses a central hub to which all nodes are connected. Because network traffic passes through the hub, the entire network fails if the hub fails to work. On the other hand, new nodes can be added without disrupting the service.

Nodes using the *ring topology* are connected in a closed loop without using a hub. Data moves from one node to the next one which examines each packet to determine whether it should be allowed to move further on to the next node. For uni-directional rings, failure of one node causes the network to shut down.

Nodes in a *mesh topology* are connected to one another, offering a choice of multiple routes for data to travel. When a node breaks down, the packet simply changes its route. This is the most expensive of all the topologies, and is found mainly in corporate networks.
