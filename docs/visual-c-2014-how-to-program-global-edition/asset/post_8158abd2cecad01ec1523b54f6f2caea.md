
# Chapter I Introduction to Computers, the Internet and Visual C#

| Name | Description |
| --- | --- |
| GPS | Global Positioning System (GPS) devices use a network of satellites to retrieve location-based information. Multiple satellites send time-stamped signals to the GPS device |

![](img/57baed2319be0bb1b5f98674846f2711_44_0.png)

## 1.3 Hardware and Software

Computers perform calculations and make logical decisions famously faster than human beings. Many of today's personal computers can perform billions of calculations in one second—more than a human can perform in a lifetime. Supercomputers are already performing trillions (quadrillions) of instructions per second! China's National University of Defense Technology's Tianhan-2 supercomputer can perform 33 quadrillion calculations per second (33.8 petaflops)¹ To put that in perspective, the Tianhan-2 supercomputer can perform in one second 3 million calculations for every planet! And supercomputing upper limits are getting quickly.

Computers consist of devices referred to as hardware (e.g., the keyboard, screen, mouse, hard disks, memory, DVD drives and processing units). Computing costs are dropping dramatically due to hardware and software technologies. Computers that filled large rooms and cost millions of dollars ago are now inscribed on silicon chips smaller than a fingernail, costing perhaps a few dollars each. Ironically, silicon is one of the most abundant materials on Earth—it’s an ingredient in common sand. Silicon-chip technology has made computing so economical that computers have become a commodity.

### 1.3.1 Moore's Law

Every year, you probably expect to pay at a little more for most products and services. The opposite has been the case in the computer and communications fields, especially with regard to the hardware supporting these technologies. For decades, hardware costs have fallen rapidly.

Every or two, the capacities of computers have approximately doubled inexpensive. This remarkable trend is often called Moore's Law, named for the person who identified it in the 1960s, Gordon Moore, co-founder of Intel—a leading manufacturer of the processors in today’s computers and embedded systems. Moore’s Law and related applications apply especially to the amount of computers have for programs, the amount of secondary storage (such as disk storage) to hold programs and over longer periods of time, and their processor speeds—the speeds at which they execute their programs (i.e., do they work). These increases make computers more capable, which puts greater demand on programming-language designers to innovate.

Similar growth has occurred in the communications fields—costs have plummeted as enormous demand for communications bandwidth (i.e., information-carrying capacity) has attracted intense competition. We know of no other fields in which technology improves so quickly and falls so rapidly. That phenomenal improvement is truly fostering

+ 1. http://www.top500.org.

### 1.3.2 Computer Organization

Regardless of differences in physical appearance, computers can be divided into various logical units or sections (Fig. 1.2).

| Logical unit | Description |
| --- | --- |
| Input unit | This "receiving" section obtains information (data and computer programs) from input devices and places it at the disposal of the other units for processing. Most user input is entered into computers through keyboards, touch screens and mice devices. Other forms of input receiving voice commands, scanning images and barcodes, reading from secondary storage devices (such as hard drives, DVD, Blu-ray Disc™ and USB flash drives—also called "thumb drives" or "memory sticks"), receiving video from a webcam and having your information from the Internet (such when you stream videos from YouTube™ or ebooks from Amazon). Newer forms of input data from GPS device, motion and orientation information from an accelerometer (a device that measures left/right and forward/backward acceleration) in a smartphone or game controller (such as Microsoft® Xbox, Wii Remote and Sony PlayStation Move) and voice input from devices like Echo and the forthcoming Google Home. |
| Output unit | This "shipping" section takes information the computer has processed and puts it on output devices to make it available for use outside the computer. Most information from computers today is displayed on screens (including touch screens), printed on paper ("going green" or played as video on PCs and media players (such as Apple’s iPads) and other devices, such as robots and "intelligent" appliances. Information is commonly output to storage devices, such as solid-state drives (SSDs), hard drives, DVD and USB flash drives. Popular forms of output are smartphone and game-controller vibration, virtual reality devices and mixed devices like HoloLens 3. |
| Memory unit | This rapid-access, relatively low-capacity—“warehouse” section retains information that has entered through the input unit, making it immediately available for processing when needed. The memory unit retains processed information until it is placed on output devices by the output unit. Information in the memory unit is volatile—it is typically lost when the computer’s power is turned off. The memory unit is often called memory, primary memory or RAM (Random Access Memory). Main memories on desktop and notebook computers contain as much as 12 GB of RAM, though 2 to 16 GB is most common. GB stands for gigabytes; a byte is approximately one bits. A bit is either a a or b. |
| Arithmetic and logic unit (ALU) | This "manufacturing" section performs calculations, such as addition, multiplication and division. |

Fig. 1.2 Units of a computer. (Part I of 2)

## 1.4 Data Hierarchy

| Logical unit | Description |
| --- | --- |
| Central processing unit (CPU) | This "administrative" section coordinates and supervises the operation of other units. The CPU tells the input unit when information should be read, the memory unit when information should be stored, and the output unit when information should be sent. Many of today’s computers have multiple processors—a *dual-core* has two, a *quad-core* has four and an *octa-core* has eight. |
| Secondary storage unit | This is the long-term, high-capacity “warehousing” section. Programs or data not being used by the other units are placed on secondary storage until needed again, possibly hours, days or years later. Information on secondary storage is persistent—it’s preserved even when the computer’s power is turned off. Secondary storage takes much longer to access than information in primary memory, but its cost is much less. Examples of storage devices include solid-state drives (SSDs), hard drives, DVD and USB flash drives, some of which hold over 2 TB (TB stands for terabytes; a terabyte is approximately one trillion bytes). Typical hard drives on desktop and notebook computers hold up to 2 TB, and some hard drives can hold up to 6 TB. |

Data items are processed by computers data hierarchy that becomes larger and more complex as we progress from the simplest data items (called “bits”) to richer data items, such as characters, fields, and so on. Figure 1.3 illustrates a portion of the data hierarchy.

Bits

The smallest data item in a computer can assume the value 0 or the value 1. It’s called a bit (short for “binary digit”—a digit that can assume one of two values). Remarkably, the impressive functions performed by computers involve only the simplest simplifications of 0s and 1s—examining a bit value, setting a bit value and reversing a bit value.

Characters

It’s tedious to work with data in the low-level form of bits. Instead, they prefer to work with decimal digits (0–9), letters (A–Z and a–z), and special symbols (e.g., $, @, %, &, *), (,), _, +, “, ?). Letters, digits and special symbols are known as characters. The computer’s character set is the set of all the characters used to write programs and represent data items. Computers represent only 1s and 0s, so a computer’s character represents every character as a pattern of 1s and 0s. C# supports various character sets (including Unicode), with
