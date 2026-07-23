![](1260031322.jpg)

![Cover Image](1260031322.jpg)

![Cover Image](title.jpg)

Copyright © 2018 by McGraw-Hill Education. All rights reserved. Except as permitted under the United States Copyright Act of 1976, no part of this publication may be reproduced or distributed in any form or by any means, or stored in a database or retrieval system, without the prior written permission of the publisher.

ISBN: 978-1-26-003132-4
MHID:      1-26-003132-2

The material in this eBook also appears in the print version of this title: ISBN: 978-1-26-003131-7, MHID: 1-26-003131-4.

eBook conversion by codeMantra
Version 1.0

All trademarks are trademarks of their respective owners. Rather than put a trademark symbol after every occurrence of a trademarked name, we use names in an editorial fashion only, and to the benefit of the trademark owner, with no intention of infringement of the trademark. Where such designations appear in this book, they have been printed with initial caps.

McGraw-Hill Education eBooks are available at special quantity discounts to use as premiums and sales promotions or for use in corporate training programs. To contact a representative, please visit the Contact Us page at [www.mhprofessional.com](http://www.mhprofessional.com).

Information contained in this work has been obtained by McGraw-Hill Education from sources believed to be reliable. However, neither McGraw-Hill Education nor its authors guarantee the accuracy or completeness of any information published herein, and neither McGraw-Hill Education nor its authors shall be responsible for any errors, omissions, or damages arising out of use of this information. This work is published with the understanding that McGraw-Hill Education and its authors are supplying information but are not attempting to render engineering or other professional services. If such services are required, the assistance of an appropriate professional should be sought.

TERMS OF USE

This is a copyrighted work and McGraw-Hill Education and its licensors reserve all rights in and to the work. Use of this work is subject to these terms. Except as permitted under the Copyright Act of 1976 and the right to store and retrieve one copy of the work, you may not decompile, disassemble, reverse engineer, reproduce, modify, create derivative works based upon, transmit, distribute, disseminate, sell, publish or sublicense the work or any part of it without McGraw-Hill Education’s prior consent. You may use the work for your own noncommercial and personal use; any other use of the work is strictly prohibited. Your right to use the work may be terminated if you fail to comply with these terms.

THE WORK IS PROVIDED “AS IS.” McGRAW-HILL EDUCATION AND ITS LICENSORS MAKE NO GUARANTEES OR WARRANTIES AS TO THE ACCURACY, ADEQUACY OR COMPLETENESS OF OR RESULTS TO BE OBTAINED FROM USING THE WORK, INCLUDING ANY INFORMATION THAT CAN BE ACCESSED THROUGH THE WORK VIA HYPERLINK OR OTHERWISE, AND EXPRESSLY DISCLAIM ANY WARRANTY, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO IMPLIED WARRANTIES OF MERCHANTABILITY OR FITNESS FOR A PARTICULAR PURPOSE. McGraw-Hill Education and its licensors do not warrant or guarantee that the functions contained in the work will meet your requirements or that its operation will be uninterrupted or error free. Neither McGraw-Hill Education nor its licensors shall be liable to you or anyone else for any inaccuracy, error or omission, regardless of cause, in the work or for any damages resulting therefrom. McGraw-Hill Education has no responsibility for the content of any information accessed through the work. Under no circumstances shall McGraw-Hill Education and/or its licensors be liable for any indirect, incidental, special, punitive, consequential or similar damages that result from the use of or inability to use the work, even if any of them has been advised of the possibility of such damages. This limitation of liability shall apply to any claim or cause whatsoever whether such claim or cause arises in contract, tort or otherwise.

## About the Author

![Images](f000V-01.jpg)

**Donald J. Norris** has a degree in electrical engineering and an MBA specializing in production management. He is currently an adjunct professor teaching an Embedded Systems course in the College of Engineering, Technology and Aeronautics, part of the Southern New Hampshire University (SNHU). He has also taught many different undergrad and grad courses mainly in the computer science and technology areas at SNHU and other regional schools for the past 33 years. Don created and taught the initial robotics courses at SNHU both on-campus and online.

Don retired from civilian government service with the U.S. Navy, where he specialized in underwater acoustics related to nuclear submarines and associated advanced digital signal processing systems. Since then, he has spent more than 23 years as a professional software developer using the C, C#, C++, Python, Micro Python, Node.JS, JavaScript, PHP, and Java languages in varied development projects. He also has been a certified IT security consultant for the last six years.

He has written and had published seven books including three involving the Raspberry Pi, one on how to build and fly your own drone, a book on the Intel Edison, one on the Internet of Things, and one on Micro Python.

Don started a consultancy, Norris Embedded Software Solutions (dba NESS LLC), which specializes in developing application solutions using microcontrollers, sensors, and actuators. The business has also recently completed several robotics projects for clients.

Don likes to think of himself as a perpetual hobbyist and geek and is constantly trying out new technologies and out-of-box experiments. He is a licensed private pilot, photography buff, amateur extra class operator, avid runner, and most importantly, a proud grandfather of three great kids, Evangeline, Hudson, and Holton.

*This book is dedicated to Dr. Peter Kachavos, my son-in-law, who is a remarkably intelligent man with an equally remarkable long medical career in service to his patients and the community. Until recently, Peter was a practicing internist with an office in Manchester, NH. He recently retired after 25 years from that practice and soon will be pursuing other interesting opportunities in the medical field.*

*Peter enjoys cooking, fine wine, traveling, and spending quality time with his family. His wife is my daughter, Shauna, and their child is my two-year-old granddaughter, Evangeline.*

*Peter and I have spent many hours discussing many topics ranging from ancient Greek artifacts to the latest technologies impacting modern society. I always look forward to those interesting and challenging discussions.*

## CONTENTS AT A GLANCE

[**1**   Introduction to the STMicroelectronics Line of Microcontrollers](#ch1.xhtml_ch1)

[**2**   STM MCU Software](#ch2.xhtml_ch2)

[**3**   STM32CubeMX Application](#ch3.xhtml_ch3)

[**4**   STM Project Development](#ch4.xhtml_ch4)

[**5**   General-Purpose Input Output (GPIO) and the STM Hardware Abstraction Layer (HAL)](#ch5.xhtml_ch5)

[**6**   Interrupts](#ch6.xhtml_ch6)

[**7**   Timers](#ch7.xhtml_ch7)

[**8**   Bit Serial Communications](#ch8.xhtml_ch8)

[**9**   Analog-to-Digital Conversion](#ch9.xhtml_ch9)

[**10**   Pulse Width Modulation (PWM)](#ch10.xhtml_ch10)

[**11**   Direct Memory Access (DMA) and the Digital-to-Analog Converter (DAC)](#ch11.xhtml_ch11)

[Index](#index.xhtml_index)

## CONTENTS

[Preface](#preface.xhtml_preface)

[**1**   Introduction to the STMicroelectronics Line of Microcontrollers](#ch1.xhtml_ch1)

[Microcomputer vs Microcontroller](#ch1.xhtml_ch1lev1)

[STM Nucleo Boards](#ch1.xhtml_ch1lev2)

[Principal MCU Components](#ch1.xhtml_ch1lev2a)

[Bit Serial Ports](#ch1.xhtml_ch1lev2b)

[Nucleo-64 Board Options](#ch1.xhtml_ch1lev2c)

[Summary](#ch1.xhtml_ch1lev3)

[**2**   STM MCU Software](#ch2.xhtml_ch2)

[Open-Source versus Commercial Proprietary Software](#ch2.xhtml_ch2lev1)

[Bare Metal Development](#ch2.xhtml_ch2lev2)

[Brief History of MCU](#ch2.xhtml_ch2lev2a)

[The MCU Toolchain](#ch2.xhtml_ch2lev3)

[Configuring a STM32 Toolchain](#ch2.xhtml_ch2lev3a)

[Summary](#ch2.xhtml_ch2lev4)

[**3**   STM32CubeMX Application](#ch3.xhtml_ch3)

[Pinout Tab](#ch3.xhtml_ch3lev1)

[MCU Alternative Functions](#ch3.xhtml_ch3lev1a)

[Integrated Peripheral (IP) Tree Pane](#ch3.xhtml_ch3lev1b)

[Creating an Example Project using CubeMX](#ch3.xhtml_ch3lev2)

[The main.c Code Listing](#ch3.xhtml_ch3lev2a)

[ARM Cortex Microcontroller Software Interface Standard (CMSIS)](#ch3.xhtml_ch3lev3)

[CubeMX-Generated C Code](#ch3.xhtml_ch3lev3a)

[Compiling and Downloading the Project](#ch3.xhtml_ch3lev3b)

[Downloading the Hex Code](#ch3.xhtml_ch3lev3c)

[Summary](#ch3.xhtml_ch3lev4)

[**4**   STM Project Development](#ch4.xhtml_ch4)

[Hello World Project](#ch4.xhtml_ch4lev1)

[Creating the Hello Nucleo Project](#ch4.xhtml_ch4lev1a)

[Adding Functionality to the Program](#ch4.xhtml_ch4lev1b)

[Compiling and Executing the Modified Program](#ch4.xhtml_ch4lev1c)

[Simple Modification for the main.c Function](#ch4.xhtml_ch4lev1d)

[Complex Modification for the main.c File](#ch4.xhtml_ch4lev1e)

[Summary](#ch4.xhtml_ch4lev2)

[**5**   General-Purpose Input Output (GPIO) and the STM Hardware Abstraction Layer (HAL)](#ch5.xhtml_ch5)

[Memory-Mapped Peripherals](#ch5.xhtml_ch5lev1)

[Core Memory Addresses](#ch5.xhtml_ch5lev2)

[Peripheral Memory Addresses](#ch5.xhtml_ch5lev3)

[HAL_GPIO Module](#ch5.xhtml_ch5lev4)

[GPIO Pin Hardware](#ch5.xhtml_ch5lev4a)

[LED Test Demonstration](#ch5.xhtml_ch5lev4b)

[Enabling Multiple Outputs](#ch5.xhtml_ch5lev4c)

[Push-Button Test Demonstration](#ch5.xhtml_ch5lev4d)

[Clock Speed Demonstration](#ch5.xhtml_ch5lev5)

[Setting the Pin Clock Speeds](#ch5.xhtml_ch5lev5a)

[Summary](#ch5.xhtml_ch5lev6)

[**6**   Interrupts](#ch6.xhtml_ch6)

[Interrupts](#ch6.xhtml_ch6lev1)

[NVIC Specifications](#ch6.xhtml_ch6lev1a)

[Interrupt Process](#ch6.xhtml_ch6lev2)

[External Interrupts](#ch6.xhtml_ch6lev2a)

[Interrupt Demonstration](#ch6.xhtml_ch6lev2b)

[Summary](#ch6.xhtml_ch6lev3)

[**7**   Timers](#ch7.xhtml_ch7)

[STM Timer Peripherals](#ch7.xhtml_ch7lev1)

[STM Timer Configuration](#ch7.xhtml_ch7lev2)

[Update Event Calculation](#ch7.xhtml_ch7lev2a)

[Polled or Non-interrupt Blink LED Timer Demonstration](#ch7.xhtml_ch7lev3)

[Test Run](#ch7.xhtml_ch7lev3a)

[Interrupt-Driven Blink LED Timer Demonstration](#ch7.xhtml_ch7lev4)

[Test Run](#ch7.xhtml_ch7lev4a)

[Multi-rate Interrupt-Driven Blink LED Timer Demonstration](#ch7.xhtml_ch7lev5)

[Test Run](#ch7.xhtml_ch7lev5a)

[Modification to the Multi-rate Program](#ch7.xhtml_ch7lev6)

[Test Run](#ch7.xhtml_ch7lev6a)

[Summary](#ch7.xhtml_ch7lev7)

[**8**   Bit Serial Communications](#ch8.xhtml_ch8)

[UARTs and USARTs](#ch8.xhtml_ch8lev1)

[USART Configuration](#ch8.xhtml_ch8lev1a)

[Windows Terminal Program](#ch8.xhtml_ch8lev1b)

[Enabling USART2](#ch8.xhtml_ch8lev1c)

[USART Transmit Demonstration Program](#ch8.xhtml_ch8lev2)

[Test Run](#ch8.xhtml_ch8lev2a)

[USART Receive Demonstration Program](#ch8.xhtml_ch8lev3)

[Test Run](#ch8.xhtml_ch8lev3a)

[Summary](#ch8.xhtml_ch8lev4)

[**9**   Analog-to-Digital Conversion](#ch9.xhtml_ch9)

[ADC Functions](#ch9.xhtml_ch9lev1)

[ADC Module with HAL](#ch9.xhtml_ch9lev1a)

[ADC Conversion Modes](#ch9.xhtml_ch9lev1b)

[Channels, Groups, and Ranks](#ch9.xhtml_ch9lev1c)

[ADC Demonstration](#ch9.xhtml_ch9lev1d)

[ADC Demonstration Software](#ch9.xhtml_ch9lev1e)

[Summary](#ch9.xhtml_ch9lev2)

[**10**   Pulse Width Modulation (PWM)](#ch10.xhtml_ch10)

[General-Purpose Timer PWM Signal Generation](#ch10.xhtml_ch10lev1)

[Timer Hardware Architecture](#ch10.xhtml_ch10lev2)

[PWM Signals with HAL](#ch10.xhtml_ch10lev3)

[Enabling the PWM Function](#ch10.xhtml_ch10lev3a)

[PWM Demonstration Software](#ch10.xhtml_ch10lev4)

[Demonstration One](#ch10.xhtml_ch10lev4a)

[Demonstration Two](#ch10.xhtml_ch10lev4b)

[Demonstration Three](#ch10.xhtml_ch10lev4c)

[Demonstration Four](#ch10.xhtml_ch10lev4d)

[Adding Functional Test Code](#ch10.xhtml_ch10lev4e)

[Test Results](#ch10.xhtml_ch10lev4f)

[Summary](#ch10.xhtml_ch10lev5)

[**11**   Direct Memory Access (DMA) and the Digital-to-Analog Converter (DAC)](#ch11.xhtml_ch11)

[DMA](#ch11.xhtml_ch11lev1)

[Basic Data Transfer Concepts](#ch11.xhtml_ch11lev1a)

[DMA Controller Details](#ch11.xhtml_ch11lev1b)

[Using HAL with DMA](#ch11.xhtml_ch11lev1c)

[Demonstration One](#ch11.xhtml_ch11lev1d)

[DAC Peripheral](#ch11.xhtml_ch11lev2)

[DAC Principles](#ch11.xhtml_ch11lev2a)

[HAL Software for the DAC](#ch11.xhtml_ch11lev2b)

[Demonstration Two](#ch11.xhtml_ch11lev2c)

[Demonstration Three](#ch11.xhtml_ch11lev2d)

[Summary](#ch11.xhtml_ch11lev3)

[Index](#index.xhtml_index)

## PREFACE

This book will serve both as an introduction to the STMicroelectronics line of STM32 microcontrollers (MCUs) and also as an easy-to-follow Getting Started Guide for readers interested in developing with a STM MCU. I will be using one of the very inexpensive STM Nucleo-64 development boards for all of the book projects, which should make it inviting for most readers to become involved with the hardware. In fact, doing the book demonstration projects is really the only way you can really be assured that you have gained a good comprehension of the material in this book.

I will state from the beginning that it is simply not possible to gain a total understanding of how a STM MCU functions by only reading this book. The manufacturer datasheets that describe individual STM MCUs are often over 1,000 pages in length, which describes the enormity of the task of trying to master the voluminous amount of information that describes these devices. Instead, the book contents focus on a few of the core components that make up a STM MCU and how to program those components to accomplish fairly simple tasks.

Some readers will have trepidation about starting to develop with what are typically considered professional grade MCUs. I wish to allay that fear and state that I have found that developing applications with at least one representative sample STM MCU to be remarkably easy and straightforward. In fact, I will state that in some aspects it is easier to develop with a STM MCU than with an Arduino or Raspberry Pi, which many readers will already be quite familiar and probably have already created projects with those boards.

Often, the single biggest issue with developing with MCUs is setting up a stable development toolchain. I will describe how to do this in a simple to follow, step-by-step process, which if you rigorously follow will guarantee that you will be able to quickly and without much trouble generate working binary programs. These programs will then be quickly downloaded into the development board for execution.

## 1

## Introduction to the STMicroelectronics Line of Microcontrollers

This chapter provides you with an introduction to the very comprehensive STMicroelectronics (STM) line of microcontrollers (MCUs). I will be focusing only on several specific controllers throughout the book, but that should provide you with an adequate representation of the functions and capabilities of the full line of STM MCUs.

### Microcomputer vs Microcontroller

I believe at the start of this book that it must make very clear the differences between a microcomputer and a MCU. The reason for this distinction is very simple: STM is a company that designs and manufacturers MCUs, not microcomputers. I think my following definition of a MCU is as good as any that I have read:

*A microcontroller is an integrated system containing a minimum of a microprocessor, dynamic and non-volatile memory, and a set of peripherals consistent with all design requirements.*

Right away, you can see from the definition that a MCU contains a microprocessor which is sometimes referred to as a microcomputer. There also must be both dynamic or volatile memory as well as nonvolatile or static memory, where the latter holds any programs or scripts necessary to run the microprocessor. Finally, there are always peripherals added to the design that allow for the input and output of digital signals. There are often additional peripherals such as timers, interrupt controllers, serial data ports, and a variety of others depending upon what requirements the MCU must meet.

I discuss all the principal MCU components below to provide you with a solid background to understand how a MCU functions. Most of the following explanations are based on the voluminous amount of information provided by STM on their microcontrollers. The reason behind STM providing such a large amount of information is to allow engineers/software developers access to all the data they need in order to incorporate STM products into original equipment manufacturer (OEM) designs and products. This approach is fundamentally different than the approach taken by suppliers of maker style boards and products, such as the Arduino, Raspberry Pi, BeagleBone, and so forth. In the case of the latter, board documentation is geared toward how to use a board in a project. The STM data is extremely specific describing items such as the nanosecond timing pulses between memory chips and processor buses. This is exactly the reason why some of the STM MCU datasheets are over 1,100 pages in length. Fortunately, the datasheet for the primary STM MCU I will be using in this book is only 138 pages. I will provide later in this chapter the website where you can download the datasheet.

### STM Nucleo Boards

MCU manufacturers such as STM have long recognized that they just couldn’t provide only chips to potential customers as most would have no way to effectively evaluate them for potential use in their products. This is the reason why the manufacturers offer relatively low-cost evaluation and demonstration boards, which have representative MCUs all setup and ready to run. STM offers a series of such boards that it calls the Nucleo line. I will be using a fairly simple Nucleo-64 board for the book projects. STM has actually embraced the maker community by marketing the Nucleo lineup as boards suitable for maker project use. These boards are very inexpensive, usually about US$10–15, which leads me to believe that STM is striving to gain a foothold in the maker community by actually subsidizing the manufacturing costs for the boards. In any case, this is a boon for makers and hobbyists and one that we should embrace.

[Figure 1-1](#ch1.xhtml_ch1fig1) shows the three basic Nucleo boards available at the time of writing this book.

![images](fig01-01.jpg)

**Figure 1-1**   *Three basic Nucleo boards.*

The boards are named Nucleo-32, Nucleo-64, and Nucleo-144 from left to right, respectively, as shown in [Figure 1-1](#ch1.xhtml_ch1fig1). The number in each name represents the number of pins present in the MCU chip. Nucleo-64 is the principal board used in this book.

## Principal MCU Components

The first component to consider is the processor or microcomputer.

### Processor

The processor used in Nucleo-32 and Nucleo-64 boards is the ARM Cortex M-4 32-bit processor. It too has a lengthy 278-page user guide available from [infocenter.arm.com/help/topic/com.arm.doc.dui0553a/DUI0553A_cortex_m4_dgug.pdf](http://infocenter.arm.com/help/topic/com.arm.doc.dui0553a/DUI0553A_cortex_m4_dgug.pdf). The actual processor circuitry is part of the STM MCU because STM has purchased intellectual property (IP) rights from the ARM Corporation in order to integrate it into its chips. However, for all practical purposes, the ARM processor is programmed using the tools and techniques promulgated by the ARM Corporation to support its processor IP. This distinction is of no consequence in our case because the software tools to be used for the book projects have all been carefully crafted and tested to work seamlessly together by STM. Any license issues have already been resolved without bothering the end user.

The following list contains some of the important specifications for the Cortex M-4 processor for interested readers:

•   Full-featured ARMv7-M instruction set, optimized for embedded applications

•   Floating point unit (FPU)

•   Low-power 32-bit processor

•   Memory protection unit (MPU)

•   Nested vector interrupt controller (NVIC)

•   Trace, breakpoint, and JTAG capabilities

•   Advanced Microcontroller Bus Architecture (AMBA)

•   Advanced High-Performance Bus (AHB5, *AHB*-*Lite*)

There are many more features to the Cortex M-4 processor as the 278-page user guide would suggest. I would also recommend Joseph Yiu’s book, *The Definitive Guide to ARM*^® *Cortex*^®*-M3 and Cortex*^®*-M4 Processors*, Third Edition, to readers who really want to delve into this processor to a great depth.

[Figure 1-2](#ch1.xhtml_ch1fig2) is a block diagram of the Cortex M-4 processor showing all of the listed items and more.

![images](fig01-02.jpg)

**Figure 1-2**   *ARM Cortex M-4 block diagram.*

STM is responsible for the design and implementation of all components outside of the box shown in [Figure 1-2](#ch1.xhtml_ch1fig2). Of course, the STM design must be compliant with the ARM processor specifications. One item missing in the figure is a clock input. The reason for it being missing is that the block diagram is from the ARM Cortex M-4 user guide, while the clock circuitry is the responsibility of STM, the MCU designer. STM has set the base processor clock frequency at 72 MHz, which appears to be very low in today’s world of multi-gigahertz clock rates for most PCs. In fact, the latest Raspberry Pi model 3 has a 1.2-GHz clock rate. But first appearances are deceiving in this case. The Cortex M-4 processor uses an extremely efficient instruction set, with three-stage pipelining, which maximizes the performance of the underlying reduced instruction set computing (RISC) that the processor employs. In addition, many common microcontroller tasks, which I discuss below, have been implemented in a combination of hardware and firmware, further improving the overall performance, while keeping the power consumption as low as possible. Power consumption and performance are two key microcontroller attributes that system designers always keep in mind. Keeping the clock rate as low as possible will always minimize the power consumed as well as increase the longevity of the chip.

### Memory

The Cortex M-4 processor uses a Harvard architecture. This means that program instructions are stored and retrieved from a memory separate and distinct from the memory that holds data. The other common computer architecture is named von Neumann in which instructions and data share a common memory. MCUs have very limited memory and take advantage of the speed-up available by using concurrent instruction and data access. Additionally, having separate memories means that the processor is no longer constrained to the same sized data widths. This means instructions can be fetched and executed in 4-byte chunks or 32 bits, while data can be simultaneously handled with 1-byte or 8-bit chunks, thus speeding up the overall throughput to and from the processor and memory. Another advantage the Harvard architecture has over the von Neumann form is that instruction prefetches can now be done in parallel with regular instruction executions, thus further speeding up the overall system performance. Finally, concurrent instruction and data access eliminates the need for data caches, which are typically used in von Neumann machines. This further reduces system complexity and power consumption.

The Nucleo-64 board used in this book is the STM MCU, model number STM32F302R8\. This chip has a 64-KB flash memory and a 16-KB static random access memory (SRAM). Yes, those are kilobytes, not mega- or gigabytes. You cannot expect to create any graphical programs that run in this limited memory space. Microcontroller programs are truly a throwback to the earliest days of computing where memory was very limited and developers had to use every available byte to store and execute programs. Having mentioned the scarce memory resources, you will be able to use a variety of modern-day graphic-based programs to develop the MCU program, but they will run on a PC. The compiled and optimized binary code will be downloaded into the MCU from the PC.

It turns out that 64 KB is plenty of space to run fairly large programs because the C/C++ cross-compiler used for this book’s projects produces optimize code, eliminating all but the essential instructions needed for the program. The 16-KB SRAM size is more than adequate for the dynamic memory requirements to support a maximum 64-KB sized program. The actual memory is integrated onto the MCU chip and its type is largely irrelevant for our purposes.

### Peripherals

The peripherals are what make the MCU viable for its intended purposes. In my microcontroller definition I stated, “a set of peripherals consistent with all design requirements.” This means that microcontrollers typically have different peripheral configurations depending upon the requirements they are designed to meet. This is a major reason why STM manufactures such a wide variety of MCUs. I will focus on the Nucleo-64 microcontroller I mentioned above and will use its set of peripherals as my discussion points. I will next need to demonstrate how the Nucleo-64 board is set up in order to fully explain how all the peripheral features function with this board.

### Nucleo-64 Board Layout

[Figure 1-3](#ch1.xhtml_ch1fig3) is a block diagram showing how the major components that make up a Nucleo-64 board are configured.

![images](fig01-03.jpg)

**Figure 1-3**   *Nucleo-64 block diagram.*

The first item you should note is that the board is actually made of two sections, the top section being a ST-LINK/V2-1 programmer and the bottom section is the STM32 MCU. The bottom section is also fitted with two sets of connectors. One set is compatible with the Arduino shield pin configuration and other set is the ST Morpho pinout configuration. There are two push buttons, B1 and B2, shown in the figure. B1 is multipurpose, while B2 is the reset push button. There is also one LED indicated in the figure; however, there are several others also which are shown in follow-on figures. The programmer section may be separated from the microcontroller section by snapping the sparse printed circuit board (PCB) joints, which can be seen in [Figure 1-1](#ch1.xhtml_ch1fig1). I would not recommend doing so because you would lose all programming capability for the MCU section. I suppose it was set up in this fashion so you could separate the sections once there was a working MCU for a specific project and there was no need for any further programming.

[Figure 1-4](#ch1.xhtml_ch1fig4) is a top view of the Nucleo-64 board with most of the components clearly annotated.

![images](fig01-04.jpg)

**Figure 1-4**   *Annotated top view of the Nucleo-64 board.*

Remarkably, there are relatively few components on the board. Most of the space is taken up by connectors, push buttons, configuration jumpers, LEDs, and the microcontroller chip. This sparse layout reflects the nature of the MCU, which is to be an embedded device without any of the niceties needed for the human-computer interface (HCI). HCI is possible with this board by using an appropriate extension board that plugs into this board

[Figure 1-5](#ch1.xhtml_ch1fig5) shows the bottom side of the Nucleo-64 board.

![images](fig01-05.jpg)

**Figure 1-5**   *Annotated bottom view of the Nucleo-64 board.*

Not much to see in this figure other than a bunch of 0-ohm resistors that may be removed if it was desired to disable certain features such as the reset and user buttons and user LED, or make hardware configuration changes to the ST-LINK programmer.

[Figure 1-6](#ch1.xhtml_ch1fig6) is much more interesting as it shows the pinouts for all the connectors on the top of the Nucleo-64 board.

![images](fig01-06.jpg)

**Figure 1-6**   *Nucleo-64 pinout diagram.*

There are two sets of pinouts shown in [Figure 1-6](#ch1.xhtml_ch1fig6), one belonging to the Arduino and the other to the ST Morpho. Connectors CN5, CN6, CN8, and CN9 belong to the Arduino set. Connectors CN7 and CN10 belong to the Morpho set. It is important to note that there are no one-to-one relationships between the sets. The Morpho connectors are two double rows of 38 pins for a total of 76 pins. The Arduino connectors are single-row connectors totaling 32 pins in all spread across four connectors.

### Arduino Connectors

[Tables 1-1](#ch1.xhtml_ch1tab1) to [1-4](#ch1.xhtml_ch1tab4), which are from the Nucleo-64 User Guide, detail the Arduino connectors with cross-references between Arduino pin terms and STM32 pins. I have provided further clarifications on some of the pin functions following each table, where I felt it was appropriate.

[Table 1-1](#ch1.xhtml_ch1tab1) details the CN6 connector pinout. Refer to [Figure 1-4](#ch1.xhtml_ch1fig4) to see the placement of CN6 on the board.

![Images](tab01-01.jpg)

**Table 1-1**   *CN6 Pinout*

Grounding pin 3 will reset the MCU. The STM32 pin designation NRST is short for non-maskable reset, which means a low on this pin is always recognized as a forcible MCU reset. Pins 2 and 4 provide 3.3 V, but I would recommend that only a very limited amount of current be drawn from these pins or you risk disrupting the board operations. Pin 5 provides 5 V, but again my same caution exists for excessive current draw. VIN is where you can attach an external power supply. The input voltage range is approximately 7 to 12 V based on the voltage regulator ratings connected to this pin. Jumper JP5 must be switched to accommodate the external power supply. Finally, the IOREF pin allows Arduino shields to adjust the I/O voltage to the 3V3 for the STM32 if those shields follow the STM specification.

[Table 1-2](#ch1.xhtml_ch1tab2) details the CN8 connector pinout. Refer to [Figure 1-4](#ch1.xhtml_ch1fig4) to see the placement of CN8 on the board.

![Images](tab01-02.jpg)

**Table 1-2**   *CN8 Pinout*

These pins are the analog voltage inputs that are routed to the MCU multichannel analog-to-digital converter (ADC). You must restrict the analog input voltage to 3.3 V or less to avoid damaging the ADC inputs. Note that there is no one-to-one correspondence between the Arduino channels and the MCU channels. Pins 5 and 6 are the default ADC inputs. If you need these to bus #1 I2C inputs, you must disconnect solder bridges SB51 and SB56 and connect SB42 and SB46\. These connections are made using 0-ohm resistors on the bottom side of the MCU board. Please note that the bus #1 I2C connections are already available on pins 1 and 2 on connector CN5.

[Table 1-3](#ch1.xhtml_ch1tab3) details the CN5 connector pinout. Refer to [Figure 1-4](#ch1.xhtml_ch1fig4) to see the placement of CN5 on the board.

![Images](tab01-03.jpg)

**Table 1-3**   *CN5 Pinout*

The analog voltage reference (AREF) should be connected to 3.3 V because that is the maximum allowed voltage to be input to the MCU ADC channels. If you have another supply available with a lesser voltage, say 2.5 V, then you can connect AREF to that and increase the ADC dynamic range by a third. Just be aware that inputting a voltage greater than 2.5 V will not change the ADC output, effectively saturating it. Pins 3 to 6 may be configured as general-purpose input/output (GPIO) or act as the bus #2 serial peripheral interface (SPI). Pins 2, 3, and 4 can also act as timer pins if neither the GPIO nor the SPI is required.

[Table 1-4](#ch1.xhtml_ch1tab4) details the CN9 connector pinout. Refer to [Figure 1-4](#ch1.xhtml_ch1fig4) to see the placement of CN9 on the board.

![Images](tab01-04.jpg)

**Table 1-4**   *CN9 Pinout*

These eight pins are normally regular GPIO, but they may be reconfigured so that pins 4, 6, and 7 are timer pins. In addition, pins 1 and 2 can act as the #2 USART.

### Morpho Connectors

[Table 1-5](#ch1.xhtml_ch1tab5) is from the Nucleo-64 User Guide and details the STM Morpho connections with references to the STM32 pins. I have provided further clarifications on some of the pin functions following the table, where I felt it was appropriate. I did not repeat the comments I provided for Arduino connection as they are equally valid for the Morpho connections.

![Images](tab01-05.jpg)

**Table 1-5**   *CN7 and CN10 Pinouts*

[Table 1-5](#ch1.xhtml_ch1tab5) details the CN7 and CN10 connector pinouts. Refer to [Figure 1-4](#ch1.xhtml_ch1fig4) to see the placement of CN7 and CN10 on the board.

U5V is 5-V power supplied from the ST-LINK/V2-1 USB connector. The BOOT0 input pin allows for changing how the MCU initially boots during a power-on event. I will discuss the boot options in a later chapter. VBAT input is often used as a battery backup for powering a real-time clock or a security key. It is typically tied to VCC if not used for a battery backup.

The next series of MCU components that I will discuss enable the MCU to perform its operations more efficiently and quickly than possible by relying on software constructs.

### Nested Vectored Interrupt Controller (NVIC)

Interrupts are essential elements in the MCU structure. Without them, MCUs cannot efficiently function given the limited memory available and low clock speeds. MCU interrupts are implemented both in hardware and software. But first I need to define what an interrupt is and how it is used:

*An interrupt is a disruption in the normal flow of a program initiated by an external or temporal event.*

[Figure 1-7](#ch1.xhtml_ch1fig7) is a flow diagram of a generic interrupt sequence. This diagram will make it easier to understand how an interrupt works.

![images](fig01-07.jpg)

**Figure 1-7**   *Interrupt flow diagram.*

ISR in [Figure 1-7](#ch1.xhtml_ch1fig7) stands for interrupt service routine, which is the program code that executes whatever needs to be accomplished due to the interrupt. The block containing the phrase “Call ISR” causes the current state or context of the MCU to be saved in SRAM. The current state typically consists of the contents of program counter (PC) and a preset number of registers that depends on the MCU model. The PC is a register, which contains the address of the next instruction to be executed when the interrupt was recognized. The actual ISR code may be located anywhere in memory because it is accessed by replacing the PC with the first address of the ISR. That address is contained in a list, which is known as the vector interrupt list. The last instruction in an ISR is always a return from interrupt, which restores the MCU’s pre-interrupt state and resumes executing instructions at the stored PC address.

The figure is slightly off target and shows a block in the ISR section containing the phrase “Enable interrupt system.” The STM NVIC uses prioritized interrupts, which means a higher priority interrupt can always interrupt a lower priority interrupt while it is executing. This normally is not possible with a purely software-implemented interrupt scheme, which is depicted by the figure’s flow diagram.

[Figure 1-8](#ch1.xhtml_ch1fig8) shows two ways the NVIC handles multiple interrupt requests (IRQs).

![images](fig01-08.jpg)

**Figure 1-8**   *NVIC handling multiple IRQs.*

I don’t believe it makes much difference on how the NVIC handles interrupts for most non-safety-related projects. However, it would be very important if a designer was creating a safety critical system. One case that came to mind was an automotive control system, in which a STM MCU was managing a variety of systems including the infotainment system and a collision avoidance system. I certainly think that a collision avoidance IRQ would need immediate attention if the MCU was processing a radio station change request at the time the higher priority IRQ was received.

The NVIC used in the Nucleo-64 MCU project board has the following specifications:

•   Sixteen interrupt lines

•   Sixteen priority levels

•   Up to 62 maskable interrupt channels

•   Low-latency interrupt processing

•   Processing of late arriving, higher priority interrupts

•   Supporting tail chaining

•   Interrupting entry restored on interrupt exit with no instruction overhead

I will discuss how to program ISRs in the software chapter.

### General-Purpose Inputs/Outputs (GPIOs)

Each of the 51 GPIO pins can be configured by software as output with push-pull or open-drain and with or without pull-up or pull-down. They can also be configured as floating input, with or without pull-up or pull-down. Most GPIO pins have peripheral alternate functions as can be seen in the above tables. All GPIOs are high-current-capable and have limited speed selection to better manage internal noise, power consumption, and electromagnetic emission.

### Analog-to-Digital Converter (ADC)

There is one 12-bit ADC that has 16 channels. ADC conversions can be done in either a single-shot or scan mode. In the scan mode, an automatic conversion is performed on a preselected group of analog inputs. An interrupt can be generated if a converted voltage is outside preset threshold. In addition, a specific channel conversion can be triggered by the TIM1, TIM2, TIM3, TIM4, or TIM5 timers.

### External Interrupt/Event Controller (EXTI)

There is an external interrupt/event controller that uses 23 edge-detector lines to generate interrupt/event requests. Each line may be independently configured to select the trigger event such as leading edge, trailing edge, or both. All these lines can be independently masked. There is a register that maintains the status of each interrupt request. The EXTI can detect an external line with a pulse width shorter than the internal main clock period. Up to a maximum of 81 GPIOs can be connected to the 16 external interrupt lines.

### Timers and Counters

Many typical MCU activities involve temporal or timing events. Using hardware timers and counters can minimize software execution cycles that are best allocated to other activities. That is why MCUs typically incorporate an array of timers and counters in their structure. Timers and counters are also tightly coupled with interrupts to provide an extremely efficient way to process timing and counting events.

[Table 1-6](#ch1.xhtml_ch1tab6) details the features supported by a single advanced control timer as well as the general purpose (GP) and basic timers.

![Images](tab01-06.jpg)

**Table 1-6**   *MCU Timer Features*

Although there are two more watchdog timers, they are not listed in the table. I discuss each timer type below.

### Advanced Control Timer (TIM1)

This timer has four independent channels that may be used for the following:

•   Input capture

•   Output capture

•   Pulse width modulation (PWM)

•   Single pulse output

It can be used as a GP 16-bit timer if desired; however, the PWM mode is especially useful for the control of standard and continuous rotation servos. This timer may also be linked with the GPx timers for event synchronization and chaining.

### General-Purpose Timers (TIMx)

There are four GP timers available for use. These timers, TIM2, TIM15, TIM17, and TIM16, are full-featured timers with 16-bit prescalars. TIM2 is the only 32-bit timer, while the rest use 16 bits. All of these timers, except for the basic, have up to four channels for the following:

•   Input capture

•   Output compare

•   PWM

•   Single pulse output

These timers can work together in a linked manner and they can also link with TIM1.

### Basic Timer (TIM6)

The remaining timer is TIM6, which is a basic 16-bit type. It has limited options and is used only for the most basic timing feature as its name implies.

### Watchdog Timers

There are two watchdog timers. The first is an independent 12-bit, count-down with an 8-bit prescalar. It is driven by a separate 32-KHz crystal, which allows it to operate independently from the main MCU clock. It also operates when the MCU is in the standby or even stop mode. This allows it to reset the MCU if an event happens that inadvertently stops the MCU.

The second watchdog timer is a free-running 7-bit downcounter that can also be set up to reset the MCU in case a problem occurs. This watchdog runs from the MCU main clock, but it does have an early-warning interrupt capability, which gracefully stops the MCU in case of an unanticipated problem.

### SysTick Timer

There is one more timer, SysTick, but it is not recommended to use. This timer is ordinarily dedicated to support real-time operating systems (RTOS). However, if the MCU project is not using an RTOS, then the timer is freely available. This timer features the following:

•   A 24-bit downcounter

•   Autoreload capability maskable system interrupt generation when the counter reaches 0

•   Programmable clock source

I would say that this timer should only be used as a last resort in the unlikely case that all the other timers have been fully committed. I cannot conceive of a project complex enough where this would happen.

## Bit Serial Ports

This MCU supports 4-bit serial protocols that allow for serial communication between it and other computing systems or peripherals.

### USART Serial Protocol

The first bit-serial protocol to be discussed is the standard Universal Synchronous/Asynchronous Receiver/Transmitter (USART). This serial protocol may or may not require a clock signal depending upon if it is configured as synchronous or not. The MCU provides two USART terminal ports; however, only one named USART2 is active and it is directly connected to another USART port on a separate MCU located on the ST-LINK portion of the Nucleo-64 PCB. There is also pin pair CN3 located on the ST-LINK that exposes the TX and RX lines.

It is possible to disconnect the USART2 link by opening solder bridges SB13 and SB14 and closing solder bridges SB62 and SB63\. If this is done, then the USART2 port on the main MCU using pins PA2 and PA3 would be connected to CN9, pins 1 and 2, as well as to CN10, pins 35 and 37, respectively. This would then provide a USART port to any compatible serial device located on an extension board.

A second USART port named USART3 can be enabled by using jumper wires between the ST Morpho connectors CN7 and CN3, located on the ST-LINK. For example, on this Nucleo-64 board it is possible to use USART3 available on PC10 (TX) and PC11 (RX). Two jumper wires would need to be connected as follows:

•   PC10 (USART3_TX) available on CN7 pin 1 to CN3 pin RX

•   PC11 (USART3_RX) available on CN7 pin 2 to CN3 pin TX

While this physically restores the USART link, I am fairly sure that the underlying ST-LINK communications software would have to be modified to use this new USART port number.

### I2C Serial Protocol

The second bit-serial protocol is the Inter-Integrated Circuit interface or I2C (pronounced “eye-two-cee” or “eye-squared-cee), which is also known as a synchronous serial data link. A clock signal is needed because it is synchronous. [Figure 1-9](#ch1.xhtml_ch1fig9) is a block diagram of the I2C interface showing one master and one slave. This configuration is known as a multidrop or a bus network.

![images](fig01-09.jpg)

**Figure 1-9**   *I2C block diagram.*

I2C supports more than one master as well as multiple slaves. This protocol was created by Philips in 1982 and is a very mature technology, meaning it is extremely reliable. Only two lines are used: SCLK for serial clock and SDA for serial data.

The STM MCU implements three separate I2C buses. These buses can operate at the standard clock rate of 100 KHz and the fast rate of 400 KHz. This clock rate can be increased by the manufacturer to a nonstandard 1 MHz. However, that would make the I2C implementation noncompliant with the protocol. [Table 1-7](#ch1.xhtml_ch1tab7) shows the Nucleo-64 pin designations for bus 1 clock and data lines.

![images](tab01-07.jpg)

**Table 1-7**   *I2C Signal Lines*

### SPI Serial Protocol

The third bit-serial protocol that I will discuss is the Serial Peripheral Interface (SPI), which is shown in [Figure 1-10](#ch1.xhtml_ch1fig10).

![images](fig01-10.jpg)

**Figure 1-10**   *SPI block diagram.*

SPI (pronounced “spy” or “ess-pee-eye”) is also known as a synchronous serial data link. It is also a full duplex protocol, meaning data can be simultaneously sent and received between the host and slave. SPI is also referred to as a Synchronous Serial Interface (SSI) or a 4-wire serial bus.

The MCU supports five SPI links in slave and master modes using full-duplex and/or simplex communication. The interfaces are labeled SPI1 to SPI5 and can use a clock rate of up to 25 Mbits/s. The data may be framed in either a byte or double-byte format. There is also automatic error correction in the form of CRC generation and verification.

[Table 1-8](#ch1.xhtml_ch1tab8) shows the Nucleo-64 pin designations for SPI2.

![Images](tab01-08.jpg)

**Table 1-8**   *SPI2 Signal Lines*

### Inter-Integrated Sound

The fourth and final bit-serial interface to be discussed is the inter-integrated sound (I2S) interface. There are five standard I2S interfaces that are multiplexed with SPI1 to SPI5\. I2S2 and I2S3 may be operated in a master or slave mode, in either simplex or full-duplex communication modes, and can be configured to operate with a 16/32-bit resolution as an input or output channel. All I2Sx interfaces can have audio sampling frequencies from 8 kHz up to 192 kHz. Finally, the master I2S clock can be output to the external DAC/CODEC at 256 times the sampling frequency when either I2S2 or I2S3 interface is configured in a master mode.

The above discussion is simply informational because I will not be demonstrating the I2S interface.

## Nucleo-64 Board Options

The following sections discuss options specific to the Nucleo-64 board and are presented to provide you with some options when working with the board.

### LEDs

LD1 is a tricolor LED located on the ST-LINK PCB and provides information concerning the state of communications between the ST-LINK, the host PC, and the main MCU. The following list shows the various LED states and the corresponding meaning:

•   Slow blinking Red/Off: at power-on before USB initialization

•   Fast blinking Red/Off: after the first correct communication between the PC and ST-LINK/V2-1 (enumeration)

•   Red LED On: when the initialization between the PC and ST-LINK/V2-1 is complete

•   Green LED On: after a successful target communication initialization

•   Blinking Red/Green: during communication with target

•   Green On: communication finished and successful

•   Orange On: communication failure

LD2 is a green LED-labeled user and connected to Arduino signal D13 (CN5/CN6), which corresponds to STM32 I/O PB13

•   When the I/O value is HIGH, the LED is on

•   When the I/O value is LOW, the LED is off

LD3 is a red LED that indicates that the Nucleo-64 board is powered on and 5-V power is available.

### Push Buttons

There are two push buttons on the board:

•   B1 USER: The user button is connected to the I/O PC13 (CN7/23) of the MCU. This pin is pulled high through a 47K resistor. When B1 is pressed the pin is grounded.

•   B2 RESET: This push button is connected to NRST, and is used to RESET the MCU.

***NOTE**The blue and black plastic hats that are placed on the push buttons can be removed if necessary, for example, when a shield or when an extension board is plugged on top of the Nucleo-64 board. This will avoid pressure on the buttons and consequently a possible permanent target RESET.*

### JP6

Jumper JP6 is labeled IDD and is used to measure the MCU current by removing the jumper and connecting an ammeter in *series* with the two pin leads.

•   Jumper ON: MCU is powered (default).

•   Jumper OFF: An ammeter must be connected to measure the MCU current. The MCU cannot receive any power if there is no ammeter connected.

### OSC Clock

There are four options on how to connect an high-speed external clock (HSE) on the Nucleo-64 board.

### Master Clock Output from the ST-LINK (Default)

The master clock output (MCO) is generated by an 8-MHz crystal located on the ST-LINK PCB and input into the main MCU via the PF0/PD0/PH0-OSC_IN pins. This crystal frequency is fixed. Incidentally, the 72-MHz clock rate I mentioned earlier in this chapter is generated by using a phase-locked loop (PLL) embedded in the MCU using the 8-MHz input clock signal.

### HSE Oscillator On-board with the Optional X3 Crystal

An 8-MHz crystal must be installed in empty X3 PCB pads. In addition, there are some solder bridges to be changed, and some resistors and capacitors to be added. The details are specified in the user’s guide.

### External Oscillator Through Pin 29 of the CN7 Connector

There are some solder bridges to be changed, and some resistors to be removed. The details are specified in the user’s guide.

### HSE Not Used

PF0/PD0/PH0 and PF1/PD1/PH1 are used as GPIOs instead of as a clock source. There are some solder bridges to be changed, and some resistors to be removed. The details are specified in the user’s guide. I am unsure how the MCU functions without an HSE, but it is an option according to the user’s guide.

### OSC 32-kHz Clock Supply

There are three ways to configure the pins corresponding to low-speed external clock (LSE).

### LSE On-board Oscillator

You can change the X2 crystal provided that it conforms to the oscillator design guide for STM32 MCU. The default crystal already installed is a model ABS25-32.768KHZ-6-T manufactured by Abracon Corporation.

### External Oscillator Through Pin 25 of the CN7 Connector

There are some solder bridges to be changed, and some resistors to be removed. The details are specified in the user’s guide.

### LSE Not Used

PC14 and PC15 are used as GPIOs instead of the LSE source. There are some solder bridges to be changed, and some resistors to be removed. The details are specified in the user’s guide. I am fairly sure that the real-time clock and watchdog timers will become inoperative with the LSE disabled.

### Power Supply and Power Selection

I have already discussed on where an external power supply may be attached in the Arduino connector. However, there are still some more power supply features and options you should know about.

### Power Supply Input from the USB Connector

The whole Nucleo-64 board including any attached extension board can be powered by the 5-V power supplied through the CN1 USB connector provided the host USB device complies with the USB standard of providing 500 mA. The ST-LINK requires 100 mA and the main MCU requires 300 mA, which leaves 100 mA for any extension board or external devices such as LEDs or LCD displays. You must use an external supply if the total current is planned to exceed a nominal 500-mA load. The red LED LD3 will not light if there is insufficient current present to power the MCU.

When the board is power supplied by USB (U5V), a jumper must be connected between pins 1 and 2 of JP5.

Jumper JP1 is configured according to the maximum current consumption of the board when powered by the USB (U5V) connection. JP1 jumper can be set in case the board is powered by USB and maximum current consumption on U5V does not exceed 100 mA (including an eventual extension board or Arduino shield). In such condition, the USB enumeration will always succeed since no more than 100mA is required from the host. Possible configurations of JP1 are summarized in [Table 1-9](#ch1.xhtml_ch1tab9).

![Images](tab01-09.jpg)

**Table 1-9**   *JP1 Configuration Table*

***NOTE**If the Nucleo-64 board is powered by an USB charger, there will be no USB enumeration from the ST-LINK causing the LD2 LED to remain off. In this case, JP1 needs to remain in place so that the MCU can be powered on.*

### VIN and E5V External Power Supply Inputs

The details and limitations of external power sources VIN and E5V are summarized in [Table 1-10](#ch1.xhtml_ch1tab10).

![Images](tab01-10.jpg)

**Table 1-10**   *VIN and E5V External Supply Input Limitations*

When the board is power supplied by VIN or E5V, these jumper configurations must be set as follows:

•   Jumper on JP5 pins 2 and 3

•   Jumper removed on JP1

### 3.3-V external Power Supply Input

It is possible to power the MCU with an external 3.3-V power supply. The power connection would be made at CN6, pin 4 or CN7, pins 12 and 16\. In this situation the 3.3-V supply is coming from an extension board. The ST-LINK will not be powered on with this configuration, thus making programming and debugging unavailable. The 3.3-V external power supply configuration is summarized by [Table 1-11](#ch1.xhtml_ch1tab11).

![Images](tab01-11.jpg)

**Table 1-11**   *3.3-V External Power Supply Configuration*

### External Power Supply Output

When powered by USB, VIN, or E5V, the 5-V supply (CN6, pin 5 or CN7, pin 18) may be used as output power supply for an Arduino shield or an extension board. In this case, the maximum current of the power source specified in [Table 1-10](#ch1.xhtml_ch1tab10) must be respected. The 3.3 V (CN6, pin 4 or CN7, pins 12 and 16) can be used also as power supply output. The current is limited by the maximum current capability of the regulator U4 (500 mA max).

[Table 1-12](#ch1.xhtml_ch1tab12) details the position of the JP5 jumper with regard to using an external power supply.

![Images](tab01-12.jpg)

**Table 1-12**   *JP5 Jumper Positions*

### Using VIN or E5V as an External Power Supply

VIN or E5V can be used as an external power supply in case the current consumption of Nucleo-64 and the extension board exceeds the maximum allowed current provided by the USB connection. It is still possible to use the USB for programming and debugging only, but it is mandatory to power-on the Nucleo-64 board first using VIN or E5V and then connect the USB cable to the host PC. Following this sequence ensures that the USB enumeration will occur when connected to an external power source.

The following power-on sequence procedure should be used:

1.   Connect the jumper between pins 2 and 3 of JP5

2.   Check that jumper JP1 is removed

3.   Connect the external power source to VIN or E5V

4.   Turn-on the external power supply VIN or E5V

5.   Check that LD3 is turned on

6.   Connect the host PC to USB connector, CN1

If this order is followed, the board may be supplied by VBUS first and then by VIN or E5V. The following risks may be encountered:

•   The host PC USB power supply can be damaged if more than 300 mA is drawn by the Nuclueo-64 board and host cannot supply it.

•   Up to 300 mA may be drawn from the host PC USB connection because JP1 is in the off position. If the host cannot supply this amount, the USB enumeration will fail and the MCU will not start.

This section concludes this introductory chapter for the STM32 Nucleo-64 board.

### Summary

This is an introductory chapter on the STMicroelectronics (STM) Nucleo-64 microcontroller (MCU) development board. This board features the model STM32F302R8 MCU, which runs at 72-MHz clock rate and has 64-KB flash and 16-KB SRAM memories.

I first reviewed the differences between a microcomputer and a MCU. A review of the principal components that make up a MCU followed next. The first component discussed was the ARM Cortex M-4 32-bit microcomputer. The next was the memory, where I briefly explained how the Cortex M-4 Harvard Architecture speeds up the processing cycle. The last component portion was an extensive discussion of the MCU peripherals.

I carefully explained how the Arduino and ST Morpho connectors were set up on the board using a series of detailed tables with additional comments. Next followed some peripheral discussions concerning an interrupt controller, timers/counters, and bit-serial interfaces.

The chapter finished up with a thorough discussion of the many board options available with which you can customize the Nucleo-64 development board to suit your own situation.

## 2

## STM MCU Software

This chapter explores the software side of MCU development. The discussion on MCU hardware in [Chapter 1](#ch1.xhtml) becomes largely irrelevant without a thorough discussion on how to use it, which is the role of software. It would be helpful to provide a bit of prospective as it pertains to the software situation as related to STM MCUs.

### Open-Source versus Commercial Proprietary Software

The first thing you need to realize is that STM is a multibillion dollar, for-profit company and must make a profit to stay in business as well as satisfy its stakeholders. Although STM does support the maker community and open-source development, it has fostered commercial software suites to be the primary means by which software is developed for their MCUs and other product lines. This means it is up to each individual maker and/or open-source developer to decide whether or not to craft your own open-source software toolchains or use a proprietary solution. I discuss both approaches and you will shortly see what my decision was and why I made that decision.

The available STM MCU commercial toolchains can be used with very little fuss but they are very expensive, with all of them costing more than $1,000 for a single license. Some software suppliers such as Keil and IAR do provide evaluation versions of their software freely available for those developers who want to try their suites out before purchasing. The only constraint with these versions is that they limit the uploaded MCU program size to 32 KB. While this limit might appear to be small, in reality, it is more than adequate for almost all projects the maker community would develop. I used the Keil evaluation IDE for all the book project code development. I have found that using this particular IDE makes developing code quite easy and with little issues that happen when attempting to develop using purely open-source tools. I want to be very clear that I am not recommending that you avoid the open-source approach, but simply stating that I have attempted both approaches and determined that using a proprietary IDE was much simpler and almost always worked the first time.

### Bare Metal Development

The phrase “bare metal development” is a fairly recent addition to the developer’s lexicography. It generally is taken to mean any low-level method of programming related to a specific hardware set. It is derived from the phrase “programming on the bare metal.” This type of development has been around since the advent of MCUs in the 1970s, when it was the only type available. It wasn’t called *bare metal development* at that time, just embedded development or simply MCU programming. It would be helpful to relate some history to understand the present state of MCU software development.

## Brief History of MCU

The Texas Instruments (TI) TMS1000 is often called the *first microcontroller*. It was released in 1971 and had read-write memory (RAM), read-only memory (ROM), an embedded 8-bit processor, and an on-board clock system. Previous to this chip, other processors relied on external memory and clock peripherals for those functions. TMS1000 was used in early TI calculators as well as some gaming consoles. Meanwhile, Intel designed and produced Intel 8048, which too had on-board RAM and ROM, as well as an 8-bit processor, clock circuitry, and some GPIO pins for direct peripheral interface. This chip turned out to be immensely popular, especially with computer keyboard manufacturers. There were millions of 8048s used in keyboards and it soon became a big revenue generator for Intel.

TMS1000 and Intel 8048 were likely programmed using the C language along with a cross-compiler, which is a software application running on a host PC that produces raw binary code suitable for use with the embedded MCU processor. The early MCUs used a masked ROM to store the program. This meant the program was first developed, tested, and then converted to a mask that was used in the MCU wafer production process. There was no ability to reconfigure a program in the field. As you might expect, the costs to create a masked MCU was very high and developers had to get it right the first time or risk very high retooling costs to change the program.

In the 1980s, MCUs started to appear with EPROMs, which stored programs that could be changed once the MCU was exposed to ultraviolet (UV) light. [Figure 2-1](#ch2.xhtml_ch2fig1) shows Intel 8751, which is UV reprogrammable version of the immensely popular 8051 MCU.

![images](fig02-01.jpg)

**Figure 2-1**   *Intel 8751 MCU.*

If look carefully at the figure, you may see the outline of a sticker that once was applied to cover the UV window. This covering was important to prevent ambient sunshine from inadvertently erasing the EPROM. The UV EPROM eventually gave way to the EEPROM, which is an electrically erasable ROM. The Intel 8052 is a MCU version that uses an EEPROM. This chip became hugely successful in the embedded development community with many millions, if not billions, being employed in a wide variety of systems, devices, and other embedded applications. In fact, Intel 8052 and certain variants are still being manufactured today. At one time, the 805x family was by far the world’s most widely used MCU line. However, I now believe smartphone MCUs have overtaken the 805x’s as the most widely used MCUs.

I include [Table 2-1](#ch2.xhtml_ch2tab1), which compares similar features between an 8052 and the STM32F302R8 MCUs used in this book. This table starkly shows huge improvements in technology in this field.

![images](tab02-01.jpg)

**Table 2-1**   *Comparison between an 8052 and STM32F302R8 MCUs*

Just remember that in its day, the 8052 was considered a very powerful MCU. In the 1990s, I had the privilege of working with a new product development team that used an 8052 development board as its main controller. I programmed the MCU using the C language. Fortunately for the team and myself, we could reprogram it very easily as bugs in the product were discovered and resolved.

### The MCU Toolchain

Embedded developers use a “toolchain” to create and debug software run on a MCU. There is no unique toolchain because what is used depends on the host computer being used, the target MCU, the development language, the linker/loader, and other various components. Generally speaking, the toolchain consists of an editor, cross-compiler, support libraries, linker/loader, and a debugger. Most of the toolchain components are often integrated into a single application called an *integrated development environment* (IDE) or they can be separate pieces for which the developer must connect and use in a proper sequence.

Using an IDE definitely helps a developer in efficiently creating code for a microcontroller because an IDE has the following:

•   An integrated source code editor

•   A means to create a software project and automatically create and store all necessary supporting files

•   A navigation scheme to quickly sort through the many files that constitute a project

•   One-step cross-compilation

•   Easy integration with appropriate load and debug applications, which in this case is ST-LINK/V2

•   Versatile debug modes

I also want to mention that the Keil IDE contains many more features than the Arduino IDE, which many readers already likely use. The Arduino IDE comes ready to use “right out-of-the box,” which makes it very convenient for most users but at the same time limits its capabilities of supporting a vast variety of different microcontrollers, and you are limited to one programming language, that being, Processing. Setting up your own, customized toolchain simply provides you a very flexible way to support your unique programming requirements.

Toolchains may be quite simple, as is the case with the Arduino IDE, or very complex, as might be the situation for a unique MCU being developed in a Linux system with open-source software. I would consider the STM32 toolchain as established in this book as moderately complex. However, one piece of good news is that the manufacturer freely provides an application that nicely supports its MCU line as far as setting up clocks and peripherals using the C language. I discuss this application named STMCube32MX in a later section. [Figure 2-2](#ch2.xhtml_ch2fig2) shows the toolchain workflow for a generic embedded development project.

![images](fig02-02.jpg)

**Figure 2-2**   *Generic toolchain workflow.*

The first step in the process is to create the source code using a text editor. Most often, the editor is an integral part of the IDE, but developers often have their own favorite editor, which they have been accustomed to use. In all cases, the source is generated using the desired computer language, which will then be used as the input to a cross-compiler. The cross-compiler is so named because it functions with the host computer’s operating system, yet produces binary code that will run on the target MCU. This newly generated binary code must then be linked with all necessary binary libraries to form a fully executable MCU program. That job is the responsibility of the linker. The fully formed and executable binary program must next be uploaded into the MCU. This is the responsibility of the loader. The loader function is often partitioned as part hardware and part software. The ST-LINK/V2 performs the load function for the Nucleo-64 development board used in this book’s projects.

The MCU can now be run with a working program and tested to see if it performs as desired. This is called debugging and is shown as a diamond in the figure. If the program works without any flaws, which does not happen very often, the MCU is ready to go into the production or release phase. However, if bugs are detected, they must be resolved and this normally means iterating all the way back to the source code and making appropriate changes at that point. The whole toolchain must then be repeated as often as necessary until the MCU functions as desired or any left-over bugs are so trivial that they can be tolerated and stay in the final program executable code. One example of a trivial bug may be that the MCU responds to a sensor event in 21 ms instead of 20 ms, but that slight deviation has no measurable impact in the overall MCU performance.

## Configuring a STM32 Toolchain

There are many ways to configure a toolchain, as previously mentioned. I have elected to use the Keil evaluation IDE, version 4.74.

***NOTE***  *I used a Windows 10 platform to host this toolchain. I did this because I determined that the ST-LINK/V2 utility worked properly with Windows as compared to using a Mac OS or a Linux environment. You can always choose to create a toolchain with a Mac or Linux host, but be prepared to encounter some compatibility problems when attempting to link and load programs from the host to the target platform.*

### Installing the Keil IDE

The latest Keil IDE is version 5; however, I decided to install an older evaluation version 4.74 of the IDE because it seems to be more stable and I had more favorable experiences in using it. You may elect to install the latest version if you so decide, but all my projects will be done with the earlier version. The executable evaluation version 4.74 is available from the following website:

[https://www.keil.com/demo/eval/armv4.htm](https://www.keil.com/demo/eval/armv4.htm)

You will first have to fill out a registration form before you are allowed to access the download page. This form is shown in [Figure 2-3](#ch2.xhtml_ch2fig3) and doesn’t appear to be too onerous and just requests some basic information about yourself and how you intend to use the application.

![images](fig02-03.jpg)

**Figure 2-3**   *Keil registration form.*

You will see the download Web page, as shown in [Figure 2-4](#ch2.xhtml_ch2fig4), once you fill out the registration form and click on the Submit button.

![images](fig02-04.jpg)

**Figure 2-4**   *IDE download Web page.*

The download file is named MDK474.exe and is a straight Windows executable of approximately 576 MB in size. I would also recommend that you just leave all the default installation parameters as they are because they worked just fine for my toolchain setup.

You should see the Keil IDE icon on the Desktop, as shown in [Figure 2-5](#ch2.xhtml_ch2fig5), once the installation is complete. Also notice that Keil brands its IDEs as uVision. You will also see the uVision tag on many files that are automatically created during the target build process. That’s all that is needed to install the Keil IDE.

![images](fig02-05.jpg)

**Figure 2-5**   *Keil IDE v4.74 icon.*

### STM32CubeMX

The manufacturer STM provides a very nice application called STM32CubeMX that helps configure its line of MCUs and demonstration boards. The STM32CubeMX utility is a GUI-based tool that helps you create custom configuration files using the C language that are especially suited to the Nucleo board being used. For instance, this utility can create all the source code required to blink the user LED (LD2) on the NUCLEO-F302R8 board, which in turn uses a STM32F302R8 microcontroller. The C language source code covers the processor clock, peripheral port, and general-purpose input/output (GPIO) configuration as well as a few more. The STM32CubeMX application can be freely downloaded from the STM website, [http://www.st.com/en/development-tools/stm32cubemx.html](http://www.st.com/en/development-tools/stm32cubemx.html). You will have to register at the STM website in order to download this software, but it is free and STM will notify you of changes and updates to their tools as they are published. This application should be downloaded into the STM32Toolchain directory as was done with all the previous applications.

[Figure 2-6](#ch2.xhtml_ch2fig6) shows the opening splash screen for the STM32CubeMX utility after it has been downloaded and installed. I would recommend that you accept all the default suggestions as you run the installer application.

![images](fig02-06.jpg)

**Figure 2-6**   *STMCubeMX opening splash screen.*

I clicked on the “New Project” button in order to show you how this utility functions. A selection page will next appear with two tabs located near the upper left-hand corner of the window. These tabs are labeled as follows:

•   MCU Selector

•   Board Selector

I next selected the MCU Selector tab and scrolled down an extensive listing of microcontrollers until I encountered the STM32F302R8 MCU, which is the type installed on the Nucleo board used in this book. [Figure 2-7](#ch2.xhtml_ch2fig7) shows the screen with this particular MCU selected.

![images](fig02-07.jpg)

**Figure 2-7**   *Selecting a specific MCU with STMCubeMX utility.*

You should notice that a nice abstract of the MCU components and features appears in the window’s upper-top section. This information is often useful to confirm that the MCU does support whatever functions you intend to implement.

The other tab labeled Board Selector will be the one most useful to support a Nucleo board demonstration project. I clicked on that tab and scrolled down in order to select the precise Nucleo board used in the book, which is the Nucleo64 NUCLEO-F302R8 board. [Figure 2-8](#ch2.xhtml_ch2fig8) shows the result of making this selection.

![images](fig02-08.jpg)

**Figure 2-8**   *Selecting the NUCLEO-F302R8 board.*

A peripheral selection panel appropriate to the selected board appears near the window’s left-hand side. You should notice that some peripherals will have any empty box appearing in the Nb column next to the peripheral name, which indicates that particular peripheral is not included on the selected board. There is also a Max column located next to the Nb column, which shows how many peripherals of a particular type are available for that specific Nucleo board. An additional handy feature is the ability to quickly download the selected Nucleo board user guide by clicking on the “Load User Manual” located near the window’s lower right-hand corner.

[Figure 2-9](#ch2.xhtml_ch2fig9) shows a very useful and convenient MCU pinout diagram for the unit installed on the Nucleo board. It shows all the pins already connected to various peripherals including the User LED, which I will demonstrate in the next chapter.

![images](fig02-09.jpg)

**Figure 2-9**   *STM32F302RE MCU pinout diagram.*

### ST-LINK

The ST-LINK software is the next part of the toolchain, which must be installed in order to start developing the Nucleo board. It is an extremely important toolchain component because it supports the USB physical link between the board and the host computer and is the only means by which software can be uploaded to the board.

The USB ST-LINK driver software must first be downloaded and installed into the host computer in order to establish a communications link between the host and the Nucleo board. This driver software is available from the same [st.com](http://st.com) website where you downloaded the STM32CubeMX utility application. The software part number from the ST website is STSW-LINK009 and the technical description is “USB driver for ST-LINK/V2 and ST-LINK/V2-1.” This particular download is a signed driver suitable for Windows 7, Windows 8, and Windows 10 for both 32- and 64-bit hosts. The downloaded driver is an archive format named “en-stsw-link009” and must be extracted from being run. Go into the newly created directory en-stsw-link009 and click on the Windows batch file named “stlink_winusb_install” to install the USB driver. You will briefly see a command window showing the installation in progress. There is no driver software icon created, so the only way to know if the driver installation successfully completed is to run the ST-LINK utility. The ST-LINK utility installation is discussed below.

The actual ST-LINK/V2 utility must be separately downloaded from the [st.com](http://st.com) website. Its part number is “STSW-LINK004” and it is approximately 22 MB in size. The downloadable archive is named “en.stsw-link004”, which must also be extracted before being installed. Ensure that the archive has been downloaded into the STM32Toolchain directory. Next, go into the newly created directory en.stsw-link004 and click on the STM32-ST-LINK Utility V4.0.0.setup application, which will install and configure the ST-LINK/V2 utility. You should see the utility opening screen, as shown in [Figure 2-10](#ch2.xhtml_ch2fig10), after you click on the ST-LINK/V2 icon appearing on the host desktop.

![images](fig02-10.jpg)

**Figure 2-10**   *ST-LINK/V2 opening screen.*

One of the first things you need to do is to check which ST-LINK firmware version is currently installed on the Nucleo board you are using. To do this, first ensure the ST-LINK utility is NOT running and then connect the Nucleo board to the host computer using a USB cable with mini-A connector that plugs into the Nucleo board and a standard type A connector that plugs into the host computer. [Figure 2-11](#ch2.xhtml_ch2fig11) shows the proper USB cable to be used.

![images](fig02-11.jpg)

**Figure 2-11**   *USB cable.*

Follow the steps below after connecting the Nucleo board to the host computer to determine the current firmware installed on the board.

1.   Open the ST-LINK/V2 utility by clicking on the desktop icon.

2.   Click on the “ST-LINK” selection located on the horizontal menu bar.

3.   Click on “ST-LINK Upgrade” selection in the sub-menu.

4.   Click on the “Device Connect” button.

[Figure 2-12](#ch2.xhtml_ch2fig12) shows the result after I clicked on the Device Connect button.

![images](fig02-12.jpg)

**Figure 2-12**   *ST-LINK firmware version display.*

Obviously, do NOT upgrade the firmware version if the reported version is more current than the one shown as the upgrade. This odd situation likely happens because the upgrade version has been hard-coded into the ST-LINK/V2 archive, which in turn is not updated as often as the firmware in newly manufactured Nucleo boards. The way around this issue that companies often use is to have a dynamic download link in their upgrade software such that the latest firmware version is always available. Apparently, STM chose not to pursue this approach, which is why this situation happens. Hopefully, it will change its upgrade technique in the near future. In any case, the firmware check, in itself, confirms that the USB communication link between the host and the Nucleo board is working properly.

The next step in the toolchain configuration is to set up a debugging tool named OpenOCD. It is not really required to install the debugger, but it may come in handy when you are trying to troubleshoot a program that doesn’t work the way you believe it should.

### OpenOCD15

The Open On-Chip Debugger (OpenOCD15) utility was designed to upload new firmware onto a STM32 Nucleo board as well as support an extensive software debugging mode. This utility was originally created by Dominic Rath, but is now maintained by the STM community, including the STM company. A Windows compatible version has been created by Liviu Ionescu and is available at [https://github.com/gnu-mcu-eclipse/openocd/releases/tag/gae-0.10.0-20170124](https://github.com/gnu-mcu-eclipse/openocd/releases/tag/gae-0.10.0-20170124). [Figure 2-13](#ch2.xhtml_ch2fig13) shows the many OpenOCD15 versions that are available to be downloaded when you go to that website.

![images](fig02-13.jpg)

**Figure 2-13**   *OpenOCD15 downloads.*

I selected the version named “gnuarmeclipse-openocd-win64-0.10.0-201701241841-setup.exe”, which is the one applicable for use with a 64-bit Windows system. This executable file is 2.19 MB in size. Download this file to the STM32Toolchain directory so that it is readily available to any toolchain application that needs it. This file is a self-contained executable, which simply needs to be run in order to install OpenOCD on your host computer. [Figure 2-14](#ch2.xhtml_ch2fig14) shows the opening splash screen for the software installation.

![images](fig02-14.jpg)

**Figure 2-14**   *OpenOCD15 opening screen.*

I recommend accepting all the default selections as the installation proceeds, which only took a minute or so for my particular situation. [Figure 2-15](#ch2.xhtml_ch2fig15) shows the completion screen after the OpenOCD setup software has finished its installation process.

![images](fig02-15.jpg)

**Figure 2-15**   *OpenOCD finish screen.*

Running the OpenOCD utility is a bit different than ordinary applications because it has been created to be a service or background program. In Unix and Linux terms, this program type is known as a daemon. There are two ways to access the program.

1.   Using the telnet utility with port 4444: OpenOCD acts like a server when a telnet link is created. It will respond appropriately when commands are received. It is strictly a command-line environment.

2.   Using the telnet utility as remote server for the GNU Project Debugger (GDB): OpenOCD implements the GDB remote protocol and may be used as a mediator component between GDB and the target platform. GDB uses the IDE’s GUI environment.

I have elected to use the telnet approach because it is simple and direct and will serve most debugging purposes. GDB is more complex and is often coupled with the Eclipse IDE, which is not being used in this toolchain.

### Establishing a Telnet Link

The very first thing that you must do prior to using telnet is to enable it on Windows 10. Unfortunately, it is not enabled by default and must be done by the user. It is a relatively easy procedure as detailed below:

1.   Enter “Control Panel” in the Search text box

2.   Click on “Programs”

3.   Click on “Program and Features”

4.   Click on “Turn Windows features on or off” found in the left-hand column

5.   Scroll down and click on the check box next to “Telnet Client”

6.   Click on the “OK” button

There is an equivalent command-line procedure to enable telnet, but I found the GUI approach just as effective.

You will next need to determine the appropriate telnet script that supports the particular board that is being used for your projects. All the available scripts currently supporting Nucleo boards are detailed in [Table 2-2](#ch2.xhtml_ch2tab2).

![images](tab02-02.jpg)

**Table 2-2**   *Telnet Scripts*

I used the configuration file named “st_nucleo_f3.cfg” because it was associated to my NUCLEO-F302R8 board.

The next part of this process is to open a terminal window. The easiest and fastest way is to enter “cmd” in the Search textbox. Type in the following two command lines into the window:

![Images](c0047-01.jpg)

Remember to use the appropriate configuration file associated with your Nucleo board.

The OpenOCD service should then respond in the terminal window with what is shown in [Figure 2-16](#ch2.xhtml_ch2fig16).

![images](fig02-16.jpg)

**Figure 2-16**   *Starting the OpenOCD service.*

Notice that an error message is shown in the OpenOCD response sequence, but I found that it was inconsequential and did not affect the program operations. However, if you do not see the responses following the error, it means that a real problem exists because no communications link was created between the OpenOCD program and the target board. This problem is usually caused by having an incorrect libusb version trying to be used by Windows. Follow the Zadig utility procedure to correct this issue.

1.   Download the Zadig utility from [http://zadig.akeo.ie/](http://zadig.akeo.ie/) for your Windows version.

2.   Connect the Nucleo board to your computer.

3.   Run the Zadig utility and select Options → List All Devices.

4.   The Nucleo board should appear in the device list combo box after a short interval.

5.   Select the WinUSB driver if it is not already listed.

6.   Click on the Reinstall Driver button as shown in [Figure 2-17](#ch2.xhtml_ch2fig17).

![images](fig02-17.jpg)

**Figure 2-17**   *Reinstall WinUSB driver dialog box.*

This action should fix the libusb driver issue. Go back and try starting the OpenOCD service as previously described.

You can now minimize the terminal window, but do not close it because the OpenOCD service will stop if you do. Open another terminal window and enter the following command:

`telnet localhost 4444`

The OpenOCD service should respond with message as shown in [Figure 2-18](#ch2.xhtml_ch2fig18).

![images](fig02-18.jpg)

**Figure 2-18**   *Opening OpenOCD response.*

There will be a prompt awaiting your input to the service. There are many ways of interacting with OpenOCD and typing in “help” will give a big response for all of the many varied commands. [Figure 2-19](#ch2.xhtml_ch2fig19) shows just the beginning portion of the help response.

![images](fig02-19.jpg)

**Figure 2-19**   *Beginning portion of the OpenOCD help request.*

For much greater details, I would highly recommend that you download the OpenOCD user guide in PDF format from [http://openocd.org/doc/pdf/openocd.pdf](http://openocd.org/doc/pdf/openocd.pdf). This is a 172-page document and currently references version 0.10.0 as of January 15, 2017.

I did try out a few commands just to see how OpenOCD worked. The first command was to halt the Nucleo board from running a program. This command was:

`reset halt`

The board was running a “blinky” type program when the command was given. It instantly stopped after I pressed the Enter key on the keyboard. The next command displayed the current contents of all the MCU registers. This command was simply:

`reg`

[Figure 2-20](#ch2.xhtml_ch2fig20) shows the impressive results of using this very simple command.

![images](fig02-20.jpg)

**Figure 2-20**   *OpenOCD reg command results after a reset.*

It is obvious that all the data registers were reset to 0 content based on the `reset` command that was given previous to the `reg` command. In [Figure 2-21](#ch2.xhtml_ch2fig21), I halted the blinky program without issuing a reset. In this case, the contents of the general-purpose registers were not reset as you can see in the figure.

![images](fig02-21.jpg)

**Figure 2-21**   *OpenOCD reg command results after a halt.*

OpenOCD also has a very handy command to examine any memory location. The location contents can be returned as a word, half-word, or byte using the commands mdw, mdh, and mdb, respectively. [Figure 2-22](#ch2.xhtml_ch2fig22) shows the results of these commands being executed on memory location 0x4000 0000.

![images](fig02-22.jpg)

**Figure 2-22**   *Memory content display commands.*

I could expand upon the OpenOCD commands, but I feel you probably understand by now that the only way to get comfortable with OpenOCD is to use it and explore its many features.

The OpenOCD installation completes the overall toolchain installation process. I will demonstrate in the next chapter how to create a new C language project using the toolchain established in this chapter.

### Summary

This chapter’s discussions provide instructions on how to set up a STM32 toolchain that will enable you to create software projects that will execute on STM MCUs and demonstration boards. Instructions were only provided for Windows-based host platforms. However, I did include a reference that shows how to set up toolchains on Mac OSX and Linux platforms.

The Keil IDE using the C/C++ languages is used for this particular toolchain.

## 3

## STM32CubeMX Application

In this chapter I present an in-depth discussion of the STM32CubeMX application, which is a free utility provided by STMicroelectronics (STM). I will also start referring to it as CubeMX to just simplify the terminology. I would also like to acknowledge a fine Leanpub eBook published by Carmine Noviello titled *Mastering STM32*. Carmine’s book was invaluable reference alongside the STM datasheets without which I could not have created this book.

CubeMX is a fairly complex utility because it is intended to encompass nearly all the microcontroller chips (MCUs) and development boards that STM offers. This is quite an amazing feat considering that there are hundreds of MCU variants and dozens of development boards that STM manufactures. The CubeMX supports these devices by automatically generating C code that developers can easily use in their programs. The generated code is designed to support specific integrated peripheral (IP) devices included on the selected MCU. CubeMX may be regarded as a MCU-centric utility because of the following features:

•   MCU selection based on the STM family, that is, F0, F1, …

•   Specific IP required for the project involving mapping MCU peripherals to a specific pinout

•   Handles specific MCU clock, power, interrupt control, ...

•   Automatically adapts pinout to package configuration

•   Manages the ST hardware abstraction layer (ST HAL)

•   Manages external libraries

•   Adaptable to a variety of IDEs

[Figure 3-1](#ch3.xhtml_ch3fig1) shows the opening screen when the application is initially launched.

![images](fig03-01.jpg)

**Figure 3-1**   *CubeMX opening screen.*

There are three choices available on the screen:

•   New Project

•   Load Project

•   Help

The New Project selection will be shortly discussed in-depth, but I do first want to briefly mention what happens with the other two selections. Clicking on Load Project will display the open file dialog box, as shown in [Figure 3-2](#ch3.xhtml_ch3fig2).

![images](fig03-02.jpg)

**Figure 3-2**   *Load Project screen shot.*

In this figure there is only one project file named Hello.ioc, which is located in a project directory that is automatically created whenever a new project is created. The project directory is named using the same name entered in the new project dialog box. The project file contains everything that CubeMX needs to reconstitute the project in order to continue with any development efforts.

Clicking on the Help selection will display the opening page of a PDF document, as shown in [Figure 3-3](#ch3.xhtml_ch3fig3).

![images](fig03-03.jpg)

**Figure 3-3**   *Opening page for CubeMX Help document.*

This PDF revision is a 261-page document that carefully details all the many features and functions contained within the CubeMX application. I would strongly recommend that you select and open this document and then save it to any convenient directory. In that way, you will always have access to the help document without needing to open the CubeMX application itself. You should also consider printing applicable portions of the document to have ready reference to appropriate material while using the application.

Clicking on the New Project selection will display a page with two tab selections. One tab is entitled MCU Selector and the other is Board Selector. Clicking on the Board Selector will cause the dialog box shown in [Figure 3-4](#ch3.xhtml_ch3fig4) to appear.

![images](fig03-04.jpg)

**Figure 3-4**   *Board Selector dialog screen shot.*

I selected a Nucleo64 as the board type and NUCLEO-F302R8 as the reference as may be seen in the figure, which matched the demonstration board I selected to use in this book. [Figure 3-5](#ch3.xhtml_ch3fig5) shows the result of selecting this particular board.

![images](fig03-05.jpg)

**Figure 3-5**   *NUCLEO-F302R8 board selection.*

There are four tabs shown in this figure, which I will discuss here one by one. These tabs, displayed from left to right, are as follows:

•   Pinout

•   Clock Configuration

•   Configuration

•   Power Consumption Calculator

### Pinout Tab

[Figure 3-5](#ch3.xhtml_ch3fig5) shows the Pinout tab display, which is divided into two parts. The right-hand side shows the selected board MCU with all predesignated peripheral and GPIO pins clearly shown. ST refers to this as the Chip view for obvious reasons. These pin designations will be explored in detail in later sections as well as later chapters. The left-hand portion of the Pinout display in [Figure 3-5](#ch3.xhtml_ch3fig5) shows all the peripheral pins as well as software MiddleWares in a tree view. Next to each tree element is a symbol, which reflects the individual status of the peripheral or software line item. I will discuss these symbols after discussing Chip view and exploring the significant amount of information that can be gained from this view.

[Figure 3-6](#ch3.xhtml_ch3fig6) is an expanded diagram of the STM32F302R8Tx MCU chip that is used as the core processor in the NUCLEO-F411RE development board.

![images](fig03-06.jpg)

**Figure 3-6**   *STM32F302R8Tx MCU.*

***NOTE***  *It will be somewhat difficult for readers of the hard copy book to follow the next discussion as the figure uses color coded pins, which are very hard to distinguish in the gray-scaled rendered images. Therefore, I will attempt to identify the pins under discussion as completely as I can, given this constraint.*

There are two fully enabled GPIO pins colored in green, which are PC13 and PB13\. PC13 is located near the top left-hand corner, while PB13 is at the lower right-hand corner. Pin PC13 is permanently connected to the development board’s user blue push button and PB13 is permanently connected to the user green LED. These connections are also noted in the diagram, as shown in [Figure 3-6](#ch3.xhtml_ch3fig6).

There are nine orange-coded pins located on all four sides of the board. An orange-coded pin indicates that a peripheral normally assigned to a specific pin has not been enabled. For example, PA2 and PA3 are located on either side of the lower left-hand corner of [Figure 3-6](#ch3.xhtml_ch3fig6) and have the peripheral USART TX and RX functions assigned to each pin, respectively. Being orange coded will mean that the CubeMX application will not automatically generate any C code that will enable the USART functions for these pins.

All of the yellow-coded pins are typically located at or near the corners of the chip and are solely dedicated to power source functions with designations such as V[dd], V[ss], V[bat], and V[ca]. These pins are strict hardware designations and cannot be programmed or reconfigured.

Finally, there are two remaining olive colored pins, BOOT and NRST, with BOOT located on the top edge and NRST located on the left edge. Like the power source pins, these two pins have dedicated MCU functions and cannot be programmed or reconfigured.

All remaining pins in the Chip view are gray-coded GPIO pins and can be initialized to suit program requirements. How this is accomplished is thoroughly discussed in the next chapter. All these pins have various functions or status outputs, which may be revealed by hovering the mouse over a particular pin. The functions and status outputs for pin PC0 as shown in [Figure 3-6](#ch3.xhtml_ch3fig6) are as follows:

•   Reset_State

•   ADC1_IN6

•   TIM1_CH1

•   GPIO_Input

•   GPIO_Output

•   GPIO_Analog

•   EVENTOUT

•   GPIO_EXTI0

It would be difficult at this point to explain each of these functions and status outputs. They are all discussed in the comprehensive STM32F302R8 MCU datasheet. The GPIO functions, however, will be discussed in the next chapter.

## MCU Alternative Functions

The STM MCU architecture allows for alternative pin mapping for various peripheral functions. Control clicking on any enabled GPIO pin such as PC13 will reveal the alternate pin mappings associated with that pin, as shown in [Figure 3-7](#ch3.xhtml_ch3fig7).

![images](fig03-07.jpg)

**Figure 3-7**   *PC13 alternative pin mappings.*

All available alternative pins will immediately be color-coded blue in response to control clicking on a selected pin. In [Figure 3-7](#ch3.xhtml_ch3fig7), the alternative pins are PA13 and PB13, but only if the alternative pin(s) are not in a reset state. Using alternative mapping allows for optimized board layout if it is inconvenient to layout a trace to the primary pin. The CubeMX will attempt to automatically resolve pin layout conflicts whenever detected by assigning a peripheral function to an alternative pin. However, by placing a logical “push pin” on a selected MCU pin will lock a desired peripheral function to a pin. These “push pins” are easily seen in the figure. These pins prevent CubeMX from enabling an alternative mapping of the locked pins. Pins locked out from alternative mapping are also color coded orange.

## Integrated Peripheral (IP) Tree Pane

The IP tree pane shown in the left-hand side of [Figure 3-6](#ch3.xhtml_ch3fig6) allows a CubeMX user an easy way to enable or disable peripherals that may be assigned to a MCU pin. The tree pane also allows the user to enable certain software middleware libraries. The tree listing uses a variety of colored icons and text to indicate the peripheral status and configuration. [Figure 3-8](#ch3.xhtml_ch3fig8) shows these colored icons and textual meanings associated with each of them. This figure is excerpted from the CubeMX user manual, which I urge interested readers to download and save. There is a wealth of information available in the 261-page PDF manual, which I simply do not have the space to cover.

![images](fig03-08.jpg)

**Figure 3-8**   *Tree pane IP icons and textual descriptions.*

### Clock Configuration Tab

The STM32 series of MCUs use a very flexible approach to configure a variety of clock sources needed for MCU operations. These sources apply to both core MCU functions and most of the peripheral functions. Clock sources and the associated phase-locked loops (PLL) are shown graphically in [Figure 3-9](#ch3.xhtml_ch3fig9), which will be displayed when you click on the Clock Configuration tab.

![images](fig03-09.jpg)

**Figure 3-9**   *Clock Configuration GUI.*

[Figure 3-9](#ch3.xhtml_ch3fig9) appears a bit daunting at first glance, but do not despair as it is really not that complicated, especially after you interact with it a few times. The STM32 clock sourcing is very much capable and flexible as compared to ordinary 8-bit MCUs.

The very first thing that must be considered is the basic clock sources. There is a high-speed clock (HSE) and a low-speed clock (LSE) used for the STM32 MCU series. These clocks may be sourced either internally or externally. These clocks will be internally sourced for all of this book’s projects; however, either one or both can be externally sourced if so desired. You must first enable the appropriate clock input pins if it desired to use external clock(s). This is done by returning to the IP tree in the Pinout view and expand the RCC section. [Figure 3-10](#ch3.xhtml_ch3fig10) shows a typical configuration for these pins.

![images](fig03-10.jpg)

**Figure 3-10**   *RCC pin configurations.*

You must return to the Clock Configuration tab once the clock input pins have been enabled and complete the clock source configurations.

There will be no need to change any of the clock configurations because they are perfectly suitable to support all book projects as they are set in their default states. I do want to caution readers who might be considering overclocking the MCU. Overclocking is a common hack that users will sometimes attempt in order to “gain” some perceived performance increase from a computer system. Overclocking is especially prevalent in gaming systems where high clock rates are thought to improve display frame rates and game performance. While this may be true for some gaming systems, the undue stress due to much higher chip heat dissipation will shorten processor life considerably. Gaming systems also employ sophisticated cooling subsystems, which are not present in the STM Nucleo board series. The bottom line is to NOT overclock as that will definitely overheat the MCU and cause it to prematurely fail.

### Configuration View Tab

The Configuration View provides an overview for all of the software configurable components including GPIOs, peripherals, and middleware. There are clickable buttons, as can be seen in [Figure 3-11](#ch3.xhtml_ch3fig11), which allow for configuration options for various components. The CubeMX application will automatically create the supporting C/C++ code that supports the desired configuration.

![images](fig03-11.jpg)

**Figure 3-11**   *Configuration View.*

There are color-coded icons and text in [Figure 3-11](#ch3.xhtml_ch3fig11), in much similar fashion to what was displayed in the IP tree pane view. [Figure 3-12](#ch3.xhtml_ch3fig12) details what the icons and text mean as they are applied to the Configuration View.

![images](fig03-12.jpg)

**Figure 3-12**   *Configuration View icons and textual descriptions.*

### Power Consumption Calculator View Tab

Clicking on the remaining tab will display an uninitialized power consumption calculator screen, as shown in [Figure 3-13](#ch3.xhtml_ch3fig13).

![images](fig03-13.jpg)

**Figure 3-13**   *Power consumption calculator (PCC).*

This PCC will allow you to calculate the following:

•   Average current consumption

•   Expected battery life

•   Average DMIPS (Dhrystone million instructions per second): It is essentially a measure of the MCU efficiency as computed using a standardized software test

•   Maximum ambient temperature (TAMAX): The maximum ambient temperature is computed based on the MCU package type, internal power consumption, and a preset 105°C maximum junction temperature

There are a series of procedural steps that are carefully detailed in the CubeMX user manual, which will lead you through a step-by-step analysis to ensure that the selected battery will handle your desired application. I will not use the PCC because all the book projects use a USB power source.

### Creating an Example Project using CubeMX

It is now time to discuss how to create a new project using the CubeMX application. First start the application and then click on The New Project selection. The opening New Project screen, as shown in [Figure 3-14](#ch3.xhtml_ch3fig14), will be displayed.

![images](fig03-14.jpg)

**Figure 3-14**   *New Project opening screen.*

Click on the Board selection tab, which should cause the Board Selection screen to be shown. Select your project board as I did in [Figure 3-4](#ch3.xhtml_ch3fig4). Double-clicking on the board selection will cause a Pinout window view to appear for the STM32F-302R8Tx MCU, as shown in [Figure 3-5](#ch3.xhtml_ch3fig5).

You will now need to click on the menu bar selection title Project in order to name your new project. Select Setting from the drop-down menu, which is shown in [Figure 3-15](#ch3.xhtml_ch3fig15).

![images](fig03-15.jpg)

**Figure 3-15**   *Project dropdown menu.*

[Figure 3-16](#ch3.xhtml_ch3fig16) shows the Project Settings window that will appear after you click on the Settings selection in the Project dropdown menu.

![images](fig03-16.jpg)

**Figure 3-16**   *Project Settings screen.*

You must first enter a name in the Project Name textbox. I used “STM32Nucleo_F302” as a project name, but you can choose anything that you like. You should ensure that the Project Location textbox displays where you desire the project folder to be stored. You can use the Browse button to find the appropriate directory. For this demonstration, I used the same location I previously used for earlier book projects. The next textbox entitled *Toolchain Folder Location* should be a directory named using the combination of the Project Location and the Project Name. Make note of this location because you will shortly need to access files that CubeMX will automatically create and store in it.

Next, ensure that you have selected “MDK-V4” as the Toolchain/IDE to use, as shown in [Figure 3-16](#ch3.xhtml_ch3fig16). This selection is very important because CubeMX cannot generate the correct C/C++ code without this being selected. In addition, ensure that the Generate Under Root checkbox is checked, which will allow the generated code to be located in the proper directories.

The default linker Settings are okay. Check that the MCU Reference textbox matches the MCU you are using. If it does not match, then the generated code cannot function with the physical MCU.

Finally, the Firmware Pack Name and Version textbox as well as the Use Default Firm Location textbox should be okay as is.

In preparation for code generation, go back and click on the Project menu bar selection and click on the Project Settings submenu selection. Next, click on the Code Generator tab and the screen shown in [Figure 3-17](#ch3.xhtml_ch3fig17) should appear.

![images](fig03-17.jpg)

**Figure 3-17**   *Code Generator screen.*

Ensure that all the radio buttons and checkboxes are selected, as shown in [Figure 3-17](#ch3.xhtml_ch3fig17). You should note that I selected the radio button to “Copy only the necessary library files” in order to minimize the size of the project as stored on the host computer. Selecting the radio button “Copy all used libraries into the project folder” would have increased the overall project folder size. In either case, the final binary file size would still be the same.

Next, return to the Project submenu as has been shown in [Figure 3-17](#ch3.xhtml_ch3fig17), but this time click on the Generate Code selection. The CubeMX will take a few seconds to generate the code with a progress bar appearing on the screen. When the code generation is completed, you should see the informational dialog box, as shown in [Figure 3-18](#ch3.xhtml_ch3fig18).

![images](fig03-18.jpg)

**Figure 3-18**   *Successful code generation dialog box.*

After you click the Open Project button, you have the Keil IDE main window with the STM32Nucleo_F302 project directories and files listing appearing in the IDE’s Project pane. This view is shown in [Figure 3-19](#ch3.xhtml_ch3fig19).

![images](fig03-19.jpg)

**Figure 3-19**   *Initial STM32Nucleo_F302 project in the Keil IDE.*

There should be four subdirectories in the Project pane named STM32Nucleo_F302, Application/MDK-ARM, Drivers/CMSIS, and Application/User, respectively. In [Figure 3-20](#ch3.xhtml_ch3fig20), I expand all the subdirectories to show you all the files contained in them.

![images](fig03-20.jpg)

**Figure 3-20**   *Project directory, subdirectory, and file list.*

Your listing should be similar, depending upon the particular MCU that you used. Don’t be dismayed by the number of directories and files. You will only be dealing with three at most in the upcoming chapter projects.

There will also be a pop-up dialog box warning you that a device was not found. This dialog box is shown in [Figure 3-21](#ch3.xhtml_ch3fig21) and is simply a consequence that the initial project load did not have a specific MCU selected.

![images](fig03-21.jpg)

**Figure 3-21**   *Device not found dialog box.*

This is easily fixed by clicking on File → Device Database, as shown in [Figure 3-22](#ch3.xhtml_ch3fig22).

![images](fig03-22.jpg)

**Figure 3-22**   *Device Database menu selection.*

Next select STMicroelectronics as the manufacturer and scroll down its rather impressive list of MCUs until you find your specific model. In my case, I did not find STM32F302R8, but did find STM32F302RB, which seems to work quite well. Maybe there will be some problems in the future, but I have not encountered any to date with this selection. [Figure 3-23](#ch3.xhtml_ch3fig23) shows the result of the STM32F302RB selection.

![images](fig03-23.jpg)

**Figure 3-23**   *STM32F302RB selection.*

Just click on the Close button because there is not a Submit or Select button.

## The main.c Code Listing

The following code listing is a file named main.c which was automatically generated by the CubeMX application based solely on the parameters and configuration settings that I entered. My purpose for this listing is to show you the basic template, which will constitute the bulk of the code for all the remaining projects in this book. In this listing is a method named main, which is where the majority of any functional code will be placed. In this template, it is intentionally empty because there is no functionality desired for this program. I am also required to show the voluminous STM disclaimer comments, which are part of STM’s copyright requirements to use this code. This disclaimer will be present in all the actual code examples presented in the book. However, it will not be expanded as shown in this listing. You can always click on a small + sign to display the disclaimer.

After the listing, I have provided some additional comments regarding the methods contained in the listing.

![Images](c0073-01.jpg)

![Images](c0074-01.jpg)

![Images](c0075-01.jpg)

![Images](c0076-01.jpg)

![Images](c0077-01.jpg)

The main method, as I have previously mentioned, contains most of the functional code required by the program. The following code snippet in the main method is what I refer to as a forever loop:

![Images](c0078-01.jpg)

The `while (1)` statement causes everything contained within its scope braces to be repeated indefinitely or as I call it “forever.” This is a necessary software construct because the majority of embedded systems do not use an operating system (OS) and any running program would simply run once and then halt and likely crash. Functional code, such as for blinking an LED, would be placed in this while loop. The automatic comments generated by the CubeMX application will help guide you in placing your own code in the proper spots.

There are also a series of method calls in main that both initialize and configure the internal peripherals and GPIO pins for the MCU. These are listed in the same sequence as they are called:

![Images](c0078-02.jpg)

There can be additional methods added to the main.c file depending upon the number and types of internal peripherals that are enabled. In addition, some extra code will have to be added to files outside of main.c to support operations such as interrupts. I will cover those cases in later chapters.

At this point, I need to discuss the ARM CMSIS software architecture in order for you to understand how the newly generated code fits in with the overall software architecture.

### ARM Cortex Microcontroller Software Interface Standard (CMSIS)

ARM, which holds the intellectual property (IP) rights to all the Cortex-based MCUs, has created an interface standard that allows for efficient cross-vendor software development. This standard is called the Cortex Microcontroller Software Interface Standard and usually abbreviated as CMSIS. CMSIS addresses a full set of development tools including compilers, run-time libraries, debuggers, and other associated tools and utilities. CMSIS consists of the following main components:

•   CMSIS-CORE: Standard application programming interface (API) covering the Cortex M0, M3, M4, and M7 processors and associated peripherals.

•   CMSIS-Driver: Peripheral driver software interfacing all applicable devices with supported middleware software. This CMSIS portion contains items such as the file systems, communication stacks, and user interfaces.

•   CMSIS-DSP: Extensive optimized library supporting different data including both fixed and floating point data types. Library is applicable to Cortex M0, M3, M4, and M7 core processors.

•   CMSIS-RTOS: A standardized API implementing a real-time operating system (RTOS). This API provides a framework that supports a variety of specific Cortex, RTOS implementations.

•   CMSIS-DAP: Debug access port (DAP) is a standardized set of firmware routines that implements debugging features optimized for Cortex processors. It connects to the CoreSight Debug Access Port to have rapid access to real-time data.

•   CMSIS-SVD: This is an extensible markup language (XML) file named System View Description (SVD), which contains peripheral descriptions suitable for use by programming language header (include) files as well as debuggers and interrupt controllers.

•   CMSIS-Pack: An XML file collection containing logical descriptions and parameters for a variety of devices. A main file named PDSC is used to extract desired data from the XML file collection.

It should be noted that the STM hardware abstraction layer (HAL), discussed in the next chapter, contains specifics only related to STM MCUs and is somewhat noncompliant with the ARM Cortex Microcontroller Software Interface Standard (CMSIS). Using the CMSIS is totally voluntary on part of vendors manufacturing ARM-based MCUs and STM has apparently decided that using HAL is the best approach in its case to handle the wide variety of MCUs and associated development boards it makes. I believe STM tried to stay compliant with the CMSIS but still needed to support its vast array of products.

## CubeMX-Generated C Code

It is now time to return to a discussion of the automatically generated code that the CMSIS framework has introduced. [Figure 3-24](#ch3.xhtml_ch3fig24) is an interesting composite of the newly generated directories that show how they are related to the various CMSIS components.

![images](fig03-24.jpg)

**Figure 3-24**   *Generated code related to CMSIS structure.*

The Application/User directory contains essentially skeleton files that present a framework that users can populate with specific code to implement a desired application. The files contained within these directories are only applicable to the Application block, as shown in [Figure 3-24](#ch3.xhtml_ch3fig24).

The Drivers/CMSIS structure contains header files with names such as core_cm3, core_cm4, and so on, which contain specific logical definitions required by the real MCU peripherals and all associated control/data registers. There are also core MCU definitions as well as interrupt controller definitions and helper functions.

The Drivers/STM32F3xx_Hal_Driver directory contains all the remaining data and parameters necessary for MCU operations not already provided in other directory files. This data covers items such as interrupt numbers, peripheral device addresses, restart vectors, and additional helper functions.

The Application/MDK-ARM contains ARM-specific startup code necessary to initialize the target MCU.

## Compiling and Downloading the Project

At this point there is sufficient initialization and configuration code to build a downloadable file suitable to be run on the target. Unfortunately, it is a null project, meaning that nothing meaningful is being accomplished by the MCU. However, it is still a useful exercise to determine if the code, as it stands, can be compiled and downloaded to the target.

[Figure 3-25](#ch3.xhtml_ch3fig25) shows where the Keil IDE build icon is located. Clicking on this icon will start the automatic build process converting the source code in the project to a binary file.

![images](fig03-25.jpg)

**Figure 3-25**   *Keil IDE build icon.*

[Figure 3-26](#ch3.xhtml_ch3fig26) shows all the intermediate results that happen during the build process. This log can be very useful in the case of errors that can happen during the build process.

![images](fig03-26.jpg)

**Figure 3-26**   *Build process log.*

You may have noticed that the final compiled and linked binary file is in an axf format. This format is not compatible to be used with the ST-LINK, which expects the download file to have a hex format. This is easily fixed by clicking on the Flash menu selection and then clicking on the Configure Flash Tools. Click on the Output tab once the flash tools selection has opened. Then click on the checkbox next to the Create HEX File selection. [Figure 3-27](#ch3.xhtml_ch3fig27) shows this selection.

![images](fig03-27.jpg)

**Figure 3-27**   *Select hex file output.*

The project must be rebuilt once the hex file has been selected. This is easily done by just again clicking on the build icon. The IDE is smart enough to understand that the source code does not have to be recompiled but simply linked again to form a hex file. The resulting hex file is clearly shown in [Figure 3-28](#ch3.xhtml_ch3fig28).

![images](fig03-28.jpg)

**Figure 3-28**   *Hex file output.*

The target can now be programmed once the hex file is created. The ST-LINK application is used to download the hex file into the target, as has been previously described in [Chapter 2](#ch2.xhtml_ch2).

## Downloading the Hex Code

You first need to open the ST-LINK application and open the appropriate hex file to be downloaded. The hex file is automatically placed into the project’s MDK-ARM subdirectory as part of the build process. You will have to browse to this directory using the ST-LINK open file feature found in the File menu selection. [Figure 3-29](#ch3.xhtml_ch3fig29) shows how the sample hex file was selected.

![images](fig03-29.jpg)

**Figure 3-29**   *Open the hex file to be downloaded.*

The target must then be connected to the host computer running the ST-LINK application using an appropriate USB cable, as has been previously discussed. You will next need to click on the Target menu selection and then click on the Connect selection. [Figure 3-30](#ch3.xhtml_ch3fig30) shows the ST-LINK window after the application is connected to the target.

![images](fig03-30.jpg)

**Figure 3-30**   *ST-LINK connected to a target.*

All that’s left is to download the hex file that has been loaded into the ST-LINK application. Click on the Target menu selection and then click on the Program and Verify selection. [Figure 3-31](#ch3.xhtml_ch3fig31) shows the Program and Verify dialog box.

![images](fig03-31.jpg)

**Figure 3-31**   *Program and Verify dialog box.*

Click on the Start button to download the hex file into the target board. The red/green LED on the Nucleo board will start flashing with alternating colors to indicate that the download operation is progressing. While the download is very quick, the LED will continue to flash. I guess the STM engineers just wanted to let users know the board was programmed. [Figure 3-32](#ch3.xhtml_ch3fig32) shows the result of a successful download.

![images](fig03-32.jpg)

**Figure 3-32**   *Successful hex file download.*

The target board should be functioning in accordance with its program. In this case, absolutely nothing will happen because no functionality was programmed. This addition of functionality to the program will be investigated in the next chapter. However, I want to ensure that the download was okay, so I previously programmed the target to flash the user LED. Once the new hex file was downloaded, the LED stopped blinking, which indirectly confirmed that the nonfunctioning program was properly downloaded.

### Summary

The chapter began with an introduction to the STM32CubeMX application, which I simply referred to as CubeMX for the remainder of the book. The application has four main portions or tabs that I thoroughly discussed. CubeMX’s purpose is to initialize and configure either STM MCUs or associated development boards, which include automatically generating C code to support the desired configuration. The automatic C code generation does not extend to any embedded application, which is still the developer’s responsibility.

A generic CubeMX project was created that did not do anything other than to provide a platform for the automatically generated C code, which supports the peripherals, clocks, communication channels, and interrupts for the specific Nucleo development board. I also presented the code contained in the main.c file and briefly discussed the contents and their operations.

I next discussed the ARM CMSIS, which most ARM vendors try to be in compliance. I also showed how the automatic C code is related to the CMSIS framework.

I showed you how to build a nonfunctioning project to prove that the toolchain works as desired. The CubeMX application created all the C code because there was no developer-responsible code required for this project. The ST-LINK application was used to download a hex file to the target platform.

The process detailed in this chapter will be repeated for all the remaining book projects, and specialized code will be added to perform all desired functions.

## 4

## STM Project Development

In this chapter I will demonstrate how to build C/C++ language projects with a STM Nucleo board using the toolchain created in [Chapter 2](#ch2.xhtml_ch2) and the CubeMX application described in [Chapter 3](#ch3.xhtml_ch3). I will be using C/C++ language to create the source code for these projects. It would be helpful, but not really required, if readers are somewhat familiar with the C/C++ language in order to achieve a better understanding of the entire process. I will go thoroughly into the example code for the “Hello World” project to help clarify what is happening with the source code for those readers who are not too proficient in using C.

### Hello World Project

The traditional and customary “Hello World” program is the one that beginning developers almost always make when starting their computer language studies. In the embedded world, this program has morphed into blinking an LED instead of displaying “Hello World!” on a monitor screen. I will demonstrate step-by-step how to create a “Hello World” project using a Nucleo64-STMF302R8 demonstration board connected to a Windows 10-based host system running the toolchain established in [Chapter 2](#ch2.xhtml_ch2). You will not benefit much from this chapter unless you have read the previous chapters and created a working toolchain and become somewhat comfortable using the CubeMX application.

## Creating the Hello Nucleo Project

The first step in creating a project is to open CubeMX application. Once the application is started, click on New Project and click on the Board tab. Select the Nucleo board that you are using. In my case, it is the NUCLEO-F302R8 board, as shown in [Figure 4-1](#ch4.xhtml_ch4fig1).

![images](fig04-01.jpg)

**Figure 4-1**   *New C/C++ Project dialog box.*

Next, double-clicking on the board selection line will cause the project pinout screen shown in [Figure 4-2](#ch4.xhtml_ch4fig2) to be displayed.

![images](fig04-02.jpg)

**Figure 4-2**   *Project pinout screen.*

The next step is to click on the Project menu item, which will result in the dropdown menu, as shown in [Figure 4-3](#ch4.xhtml_ch4fig3).

![images](fig04-03.jpg)

**Figure 4-3**   *Project dropdown menu.*

Clicking on the Generate Code selection will cause the Project Settings dialog box appear, as shown in [Figure 4-4](#ch4.xhtml_ch4fig4).

![images](fig04-04.jpg)

**Figure 4-4**   *Project Settings dialog box.*

You need to provide a name in the Project Name textbox. It should be something relevant to the intended project purpose. Also confirm that the Project Location is correct along with the Toolchain Folder Location.

It is very important that you select the MDK-ARM V4 from the Toolchain/IDE combo list. The project cannot be created without MDK-ARM V4 selection.

The default Linker Settings should be okay and the “Mcu and Firmware Package” and “Firmware Package Name and Version” should also be similar to what is shown in the figure.

Finally, ensure that the checkbox next to “Use Default Firmware Location” is checked, otherwise the IDE will not be able to create the binary file.

Do NOT click on the Ok button, but instead click on the Code Generator tab near the top of the dialog box. This should make the Project Settings/Code Generator dialog box appear, as shown in [Figure 4-5](#ch4.xhtml_ch4fig5).

![images](fig04-05.jpg)

**Figure 4-5**   *Project Settings/Code Generator dialog box.*

The radio button next to “Copy all used libraries into the project folder” will initially be selected. You should click on the radio button next to “Copy only the necessary library files” in order to minimize the size of the overall project. Neglecting to make this change will not affect the size of the final binary file, but will needlessly enlarge the project folder size.

Now you can click on the Ok button to have the CubeMX application automatically generate the C/C++ code.

After a short interval, a successful Code Generation dialog box should appear, as shown in [Figure 4-6](#ch4.xhtml_ch4fig6).

![images](fig04-06.jpg)

**Figure 4-6**   *Successful Code Generation dialog box.*

Clicking on the Open Project button will cause the Keil IDE to be opened with the newly created project shown in the Project pane to the left side of the window, as shown in [Figure 4-7](#ch4.xhtml_ch4fig7).

![images](fig04-07.jpg)

**Figure 4-7**   *Keil IDE with the new project.*

The error dialog that appears in [Figure 4-7](#ch4.xhtml_ch4fig7) has been discussed in the previous chapter and is due to the IDE not having a reference to the real target hardware. That is easily fixed by going to the Device Database, as described in [Chapter 3](#ch3.xhtml_ch3). Once that is resolved, you should expand the Project directory by clicking on the + check box. Once expanded, click on the dropdown arrow next to the Application/User subdirectory to reveal the files in that directory. Finally, double-click on the main.c file, which will display the following listing. Note that this listing is the same, as has been previously shown in [Chapter 3](#ch3.xhtml_ch3). However, I do this to provide the proper context to make the desired modifications in order to add some functionality into an otherwise nonfunctional program. Also, note that the extensive STM disclaimer commentary has been minimized to save listing space.

![Images](c0092-01.jpg)

![Images](c0093-01.jpg)

![Images](c0094-01.jpg)

![Images](c0095-01.jpg)

![Images](c0096-01.jpg)

I have chosen to provide commentary to the listing using italicized number annotations to designate those portions of the listing being discussed. Simply refer to the listing and the associated number in italics to keep track of the discussion topic.

*[1]*—Either the /* ... */ or // designate a commented line, which is ignored by the compiler. The first format allows for multiple comment lines, while the second is only for a single line. Comments are for human use as a means for the developer to explain what is happening within the source code. I strongly recommend that you always comment your programs as you see with this listing.

*[2]*—The # symbol indicates a compiler instruction or directive immediately follows. In this case the statement is `#include “main.h”` which instructs the compiler to use a header file named main.h. This particular header file is stored in a workspace header file directory because the header file name is enclosed by double quotes. The main.h contains constants, definitions, and functions that provide “understandable” names to general-purpose input/output (GPIO) pins such as LD2 for the user LED and Push Button for the user push button.

*[3]*—This header file provides all the required constants and definitions for the project code to utilize the HAL framework.

*[4]*—All methods that are called must be declared prior to use in the C/C++ language. That is the purpose of the prototype section.

*[5]*—This is the starting point for the program. The `int` in front of the main function name indicates that the main function returns an integer value. This returned value to the operating system is normally a 0 if the program terminated normally, otherwise a 1 is typically returned.

The function arguments

![Images](c0097-01.jpg)

are used only when starting values are to be supplied to the program before it starts to execute. In this case, they are not required.

*[6]*—This is the opening brace. All C/C++ functions enclose all their code between opening and closing braces. There must be a matching closing brace for this main function or else the C/C++ compiler will generate an error.

*[7]*—This statement starts a system timer that generates a SysTick every 1 ms. Note the statement ends with a semicolon, which is normally required for all C/C++ declarative statements. Omitting semicolons is a common mistake done by beginning (and not so beginning) developers.

*[8]*—This statement initializes the appropriate GPIO pin that directly controls the user LED. In this case, the GPIO pin is PA5, meaning it is one of the eight pins found in port A. There are multiple GPIO ports in STM MCUs. The exact amount depends on the particular model.

*[9]*—This is the start of an infinite loop, meaning the program will run forever until manually stopped or having the power disconnected. The 1 in the parenthesis indicates a true value. Often, developers will use a Boolean variable instead of a fixed constant, thus allowing the program to be stopped programmatically from within the scope of the `while` construct. This scope is determined by opening and closing braces, similar to what was used with the main function. This use of multiple brace pairs is known as nesting.

I will provide additional explanations regarding the code modifications.

I hope that this brief review of the main.c source code has provided you a little insight into how a C/C++ program functions.

## Adding Functionality to the Program

I will show you how to add a very simple function to this program, which will flash the onboard green user LED at a rate of once per second. The two statements to be added are shown in the following code snippet, which is the forever loop.

![Images](c0098-01.jpg)

The first statement `HAL_GPIO_TogglePin(LD2_GPIO_Port, LD2_Pin);` toggles the GPIO pin that is permanently connected to the user LED on the selected Nucleo board. Note the use of human recognizable names for both the GPIO pin connected to the LED and the associated GPIO port. That feature is made possible by the defines contained in the main.h file, which is included in the main.c file.

The second statement `HAL_Delay(500);` pauses the processor for 500 ms before the LED state changes. This will cause the LED to blink once per second with a 50% duty cycle, meaning it is on for 0.5 s and off for 0.5 s.

## Compiling and Executing the Modified Program

Just click on the build icon after you added the additional two statements in the forever loop. Also, ensure you have enabled the hex file output, as described in the previous chapter. This is required prior to using the ST-LINK utility.

Again, follow the ST-LINK detailed instructions provided in [Chapter 3](#ch3.xhtml_ch3) on how to load the hex file and download it into the target board.

The user LED should immediately start to blink once the hex file is downloaded. I am fairly confident that you should have no problem with this procedure given that the program built successfully.

## Simple Modification for the main.c Function

The simplest modification to the main.c function is to change the LED timing duration, which is what I have done for this next demonstration. The following code snippet shows the modifications made to the on and off LED timing duration. It was changed to 2 s:

![Images](c0099-01.jpg)

The source code in the main.c file was first changed and then saved. I then rebuilt the project, which in turn generated a new hex file. This hex new file was then loaded into the ST-LINK utility and subsequently downloaded into the Nucleo board using the process I previously described. I immediately observed that the user LED was then flashing at a rate of 2 s on and 2 s off after the new hex file was downloaded into the target.

## Complex Modification for the main.c File

The next demonstration is a bit more complex than the previous one in that I want to show you how to blink the LED with different on and off times. I will still be using the user LED LD2 as the light source but will modify the main.c file to incorporate two different timing intervals.

I choose to use several define statements to create different on and off durations for the LED. The main function also uses an if/else statement that causes the on and off intervals to alternate based on the truth value of a Boolean variable named sw. The following is the code snippet for the modified portion of the main.c file:

![Images](c0099-02.jpg)

![Images](c0100-01.jpg)

After the main.c file was modified, the project was built in the manner previously described and the resultant hex file was downloaded into the Nucleo board using the ST-LINK utility. The user LED immediately started blinking on for 0.5 s and off for 1.5 s for a net 2-s blink rate. The on and off durations may easily be modified by changing the appropriate define statements.

This last demonstration project concludes this initial discussion on how to create and modify embedded software projects for a STM Nucleo-64 board. The next chapter explores how to use additional GPIOs and the use of interrupts, which will greatly expand the capabilities of the Nucleo board.

### Summary

This chapter contains three demonstration C/C++ language projects that all blinked an on-board LED installed on a Nucleo64-STM32F302R8 board. Each project progressed in complexity from an extremely simple constant rate LED flashing to a more complex multi-interval flashing of the LED.

I explained using a step-by-step approach how to conduct a project build. The final hex file created by the build process was downloaded into the Nucleo-64 board using the ST-LINK utility.

A brief discussion of how a C/C++ main function works was also presented for readers who might be a bit “rusty” on their C/C++ language prowess.

## 5

## General-Purpose Input Output (GPIO) and the STM Hardware Abstraction Layer (HAL)

As the formidable title states, this chapter deals with how GPIO operates on a STM Nucleo-64 board and how the HAL software is involved. It is important to first study the STM MCU architecture in order to fully understand how the GPIO ports function and their relationship to HAL. I would also acknowledge that many of the figures and table content are sourced from either the STM32F302R8 datasheet or reference manual. I would highly recommend that you download and have them readily available to help fill in any gaps in my discussions.

[Figure 5-1](#ch5.xhtml_ch5fig1) is the STM32F302R8 block diagram, which is the MCU used in the Nucleo-64 development board used in this book.

![images](fig05-01.jpg)

**Figure 5-1**   *STM32F302R8 block diagram.*

Note that there are six banks of GPIO ports shown on the left side of [Figure 5-1](#ch5.xhtml_ch5fig1), which are connected to the bidirectional advanced high-speed bus 1 (AHB1). This bus transfers digital data internally at a rate up to a maximum of 100 Mbps. HAL effectively manages the data transfers from the GPIO ports as well as from the many other peripheral components depicted in the figure.

I will start the HAL discussion by examining perhaps the simplest HAL module, which is the HAL_GPIO. This module has already been used multiple times in programs discussed in earlier chapters. The HAL_GPIO module was used without explanation simply because it was necessary to implement a required function such as blinking an LED or reading the state of a push-button switch. I will shortly closely examine the HAL_GPIO module, but first I will discuss the concept of memory-mapped peripherals.

### Memory-Mapped Peripherals

STM MCU peripherals are controlled and data is transferred using addresses within a 32-bit range. This is known as memory mapping because it makes no difference from a programming perspective whether it is communicating with a memory location or a peripheral register. The 32-bit address range is usually represented by eight integer digits, meaning the total possible range of locations is 0x0000 0000 to 0xFFFF FFFF. Note that the hex number is preceded by a 0x and a space is paced after four of the leading hex digits. The 0x is a common programming construct indicating that the number is in a hex format and the space between the two hex number groups is just to make the number more readable. This address format is also used throughout the STM documentation.

[Figure 5-2](#ch5.xhtml_ch5fig2) shows the major blocks that constitute the entire 32-bit address range.

![images](fig05-02.jpg)

**Figure 5-2**   *Complete 32-bit STM address range.*

Also shown in [Figure 5-2](#ch5.xhtml_ch5fig2) are two breakout blocks, which detail the core memory locations as well as the peripheral/bus locations. I will next briefly discuss the core memory locations, which are important in their own right, but not very relevant to the peripheral address locations.

### Core Memory Addresses

[Table 5-1](#ch5.xhtml_ch5tab1) shows the types of memory and their preassigned memory addresses.

![images](tab05-01.jpg)

**Table 5-1**   *STM Core Memory Address Ranges*

One question that many readers might be pondering is how a PC can handle 8, 16, or even 32 GB of SRAM with only 32 bits of addressing capability? The answer lies in using both an operating system designed for extended memory accesses and a hardware unit known as a memory management unit (MMU). All the major PC OSs such as Windows, OSX, and Linux have extended memory functionality built-in that allows for 32-bit addressing to extend into multiple blocks or pages. You could think of using a 4-bit register, where each bit would activate a particular block or page. Therefore, bit 0 would allow access to all the base addresses starting at 0x0000 0000, while bit 1 would allow addressing to virtually start at 0x0001 0000 0000\. Of course, there are only 32 real bits being used, but the OS handles the addresses as if they started one location beyond 0xFFFF FFFF. This 4-bit register can be thought of as being part of the MMU. Four bits means that a maximum of 64 GB can be handled in a 32-bit PC, which coincidentally is often the maximum SRAM that may be installed in such a PC. Of course, all practical physical memory limitations are relieved when a 64-bit system is used, but that requires an expensive CPU and additional energy requirements.

The preceding discussion is not applicable to a typical STM MCU because memory is quite constrained and vast amounts are not needed to handle typical embedded applications. I do want to mention that STM32F302R8 does incorporate a memory protection unit (MPU). The MPU is not a MMU, but is provided to manage CPU memory accesses such that one task will not accidentally corrupt or conflict with another task’s memory accesses. Memory can be arranged in up to eight areas with each area sized between 32 B and 4 GB, the last comprising the whole addressable memory range. The MPU is normally controlled by a real-time operating system (RTOS), which has an API contained within the CMSIS, which has been introduced in the last chapter. I will not be using the MPU for any of the book projects. You should consider its use only for the most safety-critical or mission-essential applications. Think of it being used in automotive or flight safety systems.

### Peripheral Memory Addresses

[Figure 5-3](#ch5.xhtml_ch5fig3) shows the beginning portion of the memory addresses allocated to the STM32F302R8 peripherals,

![images](fig05-03.jpg)

**Figure 5-3**   *Beginning portion of the STM32F302R8 peripheral allocations.*

You should be able to see that the AHB2 bus has the address range 0x4800 0000 to 0x4FFF 17FF. What is specific to this chapter’s focus is the total GPIO range of 0x4002 0000 to 0x4002 0x1FFF, which is divided into six smaller 1-KB blocks. Five of the six 1-KB blocks are allocated to GPIO ports A, B, C, D, and F, respectively. There is an unused block at range 0x4800 1000 to 0x4800 13FF, which has no significant impact on the port allocations. I have no idea why there is a reserved block allocated in what was a contiguous block allocation or why the final GPIO port is labeled F instead of E, as one might expect from the prior port designations. The port memory designation and allocation question probably can only be answered by the STM MCU chip designers. It is up to MCU users to accept the designations and allocations as they are and work with them to the best of their abilities.

I elected to include the following figure on peripheral locations for completeness sake and to provide a readily available reference for additional peripherals. [Figure 5-4](#ch5.xhtml_ch5fig4) shows the peripherals connected to the internal advanced peripheral bus 1 (APB1). The peripherals connected to the bus are as follows:

![images](fig05-04.jpg)

**Figure 5-4**   *AHB1 peripheral allocations.*

•   Timers (TIMxx)

•   Universal Synchronous/Asynchronous Receiver/Transmitters (USARTx)

•   Serial peripheral interfaces (SPIx)

•   Inter-integrated interfaces (I2Cx)

•   Universal serial bus (USB)

•   Integrated sound interface (I2S)

•   Digital-to-analog converter (DAC)

•   Controller area network interface (CAN)

•   Real-time clock (RTC)

•   Watch dog timers (IWDG, WWDG)

I will now return to the HAL_GPIO discussion after introducing to the concept of peripheral memory-mapped addresses.

### HAL_GPIO Module

It would be wise to examine a sample GPIO circuit before discussing how it functions with the module software. It is always an important step to understanding the underlying hardware that implements the software.

## GPIO Pin Hardware

[Figure 5-5](#ch5.xhtml_ch5fig5) is a block diagram, which also contains schematics that model a typical STM GPIO port pin.

![images](fig05-05.jpg)

**Figure 5-5**   *Typical STM GPIO port pin block diagram/schematic.*

Starting from the right-hand side of [Figure 5-5](#ch5.xhtml_ch5fig5) you can see the I/O pin, which has robust overvoltage protection circuits attached. The GPIO pin is protected up to an applied 5-V input level in spite of the fact that the main MCU voltage supply is 3.3 V and the core processor voltages are 1.8 V. This makes interfacing quite easy without the need to employ voltage level shifters or resistance voltage dividers. The I/O pin is simultaneously connected to both input and output drivers as shown in the figure. However, only one driver at a time can be activated. Inspecting the input driver section reveals three possible inputs that may be sent to the core MCU. These are as follows:

•   Analog: Bypasses the Schmitt trigger

•   Alternate function: Schmitt trigger output

•   Read: Output from one of the associated read register lines

The GPIO pin configuration settings determine which input is used at a given time.

Likewise, the output section has multiple ways of creating a signal output for the I/O pin. These are as follows:

•   Write: Output from an associated write register line. The output register also has a R/W control line.

•   Alternate function: Generated from an internal MCU peripheral.

Note that the output control block has two MOSFET transistors connected to the output control circuitry, which provide for the following operations:

•   Push-pull

•   Open-drain

•   Disabled

Finally, the I/O pin has programmable enabled resistors attached to the pin, which will allow for the following:

•   Pull-up

•   Pull-down

•   Neither

This sample circuitry is replicated for every GPIO pin existing in the MCU.

Each GPIO port has several registers attached to it, which control all of its pins’ behaviors by setting or resetting bits associated with the respective pins. [Figure 5-6](#ch5.xhtml_ch5fig6) shows the format for the GPIO port mode register for ports A … E and H.

![images](fig05-06.jpg)

**Figure 5-6**   *GPIO port mode register.*

This register would be programmatically accessed by using the symbol GPIOx_MODER where x = A … E and H for the targeted port. The power-on reset values automatically placed in all the GPIO registers are as follows:

•   0x0C00 0000 for port A

•   0x0000 0280 for port B

•   0x0000 0000 for all other ports

The di-bit or two bit values that can be stored in a register have the following meanings:

•   00—Input mode

•   01—Output mode

•   10—Alternate function mode

•   11—Analog mode

Additional GPIO registers further configure other behaviors that are associated with the port pins including the following:

•   Enabling push-pull, open-drain, or none (also called floating)

•   Enabling pull-up, pull-down, or none

•   Operational speed

The next two figures concisely display all the registers involved in all GPIO configurations. These figures are very important and will serve as the basis for configuring GPIO ports for all future projects. I had to break the GPIO register’s listings into two separate figures due to the number of involved registers. [Figure 5-7](#ch5.xhtml_ch5fig7) shows the first nine registers in order of their offset addresses to the base MODER address.

![images](fig05-07.jpg)

**Figure 5-7**   *First nine GPIO registers’ details in order of offset addresses.*

The last nine registers in the offset address order are shown in [Figure 5-8](#ch5.xhtml_ch5fig8).

![images](fig05-08.jpg)

**Figure 5-8**   *Last nine GPIO registers’ details in order of offset addresses.*

The key to reading these figures is to understand what each register is supposed to control, its offset address, and how individual GPIO pins are accessed in the register.

I will next demonstrate a simple program that will control an LED attached to port A, pin PA10.

## LED Test Demonstration

The purpose of the following demonstration is to show how to configure the port A GPIO registers to directly control an LED. The demonstration program will not blink the LED and you have to change the source code, recompile, and reload to affect the LED state.

However, there is a bit of hardware preparation that must be done before the test program can be run. That involves connecting the LED with a current limiting resistor to the selected port A pin. To ease this requirement, I elected to use an Arduino prototyping board, which is shown in [Figure 5-9](#ch5.xhtml_ch5fig9). This board is quite inexpensive and is readily available from a number of online sources.

![images](fig05-09.jpg)

**Figure 5-9**   *Arduino prototype board.*

You will also need an LED and a 330-Ω 1/4-watt resistor to limit the current flowing through the LED. It will also be important to know which GPIO pins are exposed in the Arduino protoboard. This is easily answered by referring to the STM Nucleo-64 board user manual. [Figure 5-10](#ch5.xhtml_ch5fig10) comes from that manual and shows the STM32F302R8 pins associated with both the Arduino and Morpho connectors. In our case, only the Arduino pins are needed.

![images](fig05-10.jpg)

**Figure 5-10**   *Arduino/Morpho pin connectors.*

I arbitrarily selected PA10 as the LED output, simply because it was not already configured to a peripheral in the main.c template program. [Figure 5-11](#ch5.xhtml_ch5fig11) is the schematic used for this setup.

![images](fig05-11.jpg)

**Figure 5-11**   *LED test schematic.*

The longest LED lead is connected to the anode and the shortest lead is connected to the cathode. I simply soldered the resistor and the LED together because this arrangement allowed me to easily connect the LED/resistor combination to the protoboard, as shown in [Figure 5-12](#ch5.xhtml_ch5fig12). The protoboard is also plugged into the Nucleo-64 board for this photograph.

![images](fig05-12.jpg)

**Figure 5-12**   *LED/resistor combination plugged into the protoboard.*

It is time to work on the software once the hardware is all set.

### LED Test Program

As I have previously mentioned, all STM peripherals, including GPIO ports are controlled by configuring a series of related registers, as detailed in [Figures 5-7](#ch5.xhtml_ch5fig7) and [5-8](#ch5.xhtml_ch5fig8). In this demonstration program I will be configuring pin PA10, which is in the Port A GPIO bank of pins. PA10 will need to be configured as an output. I will be using a slightly modified main method created in the previous chapter’s project. You should set up a new project with this main method and simply modify the method by entering the following two lines and making two changes to the `MX_GPIO_Init(void)` method as detailed below.

Enter these two statements immediately after the first `MX_GPIO_Init(}` statement:

![Images](c0115-01.jpg)

![Images](c0116-01.jpg)

The HAL library relies on C structure named GPIO_InitStruct to configure any GPIO pin. Using this structure hides the necessity to use actual memory-mapped addresses to configure a GPIO pin. The following code segment from the `MX_GPIO_Init(void)` method shows how the structure is initialized to configure PA10 to an output pin:

![Images](c0117-01.jpg)

The last list statement is not part of the structure initialization but is required to apply the newly initialized structure within the HAL framework. The structure components are directly related to the memory-mapped GPIO registers, as shown in [Table 5-2](#ch5.xhtml_ch5tab2).

![images](tab05-02.jpg)

**Table 5-2**   *GPIO_InitStruct to GPIO Register Equivalence*

![Images](c0117-02.jpg)

![Images](c0118-01.jpg)

![Images](c0119-01.jpg)

![Images](c0120-01.jpg)

![Images](c0121-01.jpg)

You should notice that the main method code listing ends with a `while (1)` statement, which simply forces the MCU to loop forever after the LED is turned on. The only way to turn off the LED is to disconnect the power to the board. Resetting the board will only immediately turn on the LED.

### Test Run

You will first need to compile the project in preparation for uploading into the Nucleo-64 board. You then use the ST-LINK utility to transfer the hex file from the project’s Debug directory into the Nucleo, as previously described in [Chapter 4](#ch4.xhtml_ch4). The LED should immediately turn on once the hex file is loaded into the board. Recheck the main.c code if the LED fails to turn-on. Incidentally, recheck that you have inserted the hardware into the proper pin sockets. Sometimes, it is as simple as that to fix a problem.

## Enabling Multiple Outputs

It is relatively easy to modify the main.c file to enable multiple outputs. I selected GPIO PA6 as an additional output to control an LED. Incidentally, I referred to the defines contained in the main.h file to determine the pins already committed in the project. I have included the relevant portion of the file in the following listing for your use. Note that PA10 was not added as a define; I would have added that if I were building a permanent program instead of a transient demonstration program. The same is true for pin PA6.

![Images](c0122-01.jpg)

Make the following changes to enable the multiple LED outputs.

In the `main` method change:

![Images](c0122-02.jpg)

![Images](c0123-01.jpg)

You will need to recompile and upload the new hex file into the Nucleo-64 board to test the new functionality.

### Test Run

I left the LED/resistor combination connected between PA10 and ground to recheck that it turned on when the program was loaded. It is always wise to do that type of check because it sometimes happens that unintended things happen when a program modification is done, which is believed to not affect an existing and tested function. I next disconnected the LED/resistor circuit and reconnected it to PA6 and ground and confirmed that it also turned on the LED.

It would be straightforward to enable even more outputs using the same procedure. Just note that you would need to enable another GPIO port bank if you were to use all of the available pins in the GPIOA port.

## Push-Button Test Demonstration

This demonstration will show you how to enable a GPIO pin input to detect when a user presses the blue user push button. An LED will light for as long as the push button is pressed. There is no additional hardware required for this demonstration other than what was needed for the previous LED demonstration. I will also be using GPIOA PA10 as an output pin to control the LED.

The `MX_GPIO_Init(void)` method has already configured the blue user push button, so all that is needed is to read the button state in the `main()` method. This is accomplished using the following statement:

`HAL_GPIO_ReadPin(GPIOC, GPIO_PIN_13)`

You should also recall from the [Chapter 4](#ch4.xhtml_ch4) discussion that the blue user push button is connected to GPIO Port C, pin 13 and it is also constantly being pulled high. This means the button state will be high when not pushed and transition to a low value when pushed. The corresponding C snippet must continuously respond to this event as follows:

![Images](c0124-01.jpg)

Enter the above code segment in the `main()` method to continue with the demonstration. Next compile and upload the hex file to the Nucleo-64 board.

### Test Run

I observed that the LED turned on for as long as the push button was depressed. Note that you will have to use a small screwdriver to press the button as it is hidden under the Arduino protoboard.

The next demonstration concerns a basic property involved with all MCU signal operations, including the GPIO pins.

### Clock Speed Demonstration

Clock speed as related to MCU signal operations is a misnomer. You would ordinarily consider it to be a measure of the maximum number of signal transitions per second. However, it is really a measure of the clock skew or amount of time it takes to transition a signal from 10% to 90% of the maximum value. It also applies in the opposite direction or going from 90% to 10% of the maximum value. The former is known as leading edge delay and the latter is called trailing edge delay.

Clock skew is directly related to true clock speed because the leading and trailing edge delays ultimately determine the maximum possible number of signal transitions per second. I will still refer to clock skew as clock speed because that is how STM choose to label this important signal property.

The important question that one should ask is why should clock speed even be considered. The answer lies in extending both MCU and battery life. The physics behind improving clock speed dictates that it takes energy or power, in this case, to overcome the circuit capacitance effects that mainly determine clock speed. Small amounts of additional power are required to improve the circuit switching times. This implies an increase in current flow from the battery over time and consequently a shortened battery life. In addition, increased power dissipation will induce small amounts of additional heat stress in the MCU and also shorten its life. The aforementioned are the main reasons why clock speed should always be selected to be the lowest level but still support required functionality.

This demonstration will illustrate the actual clock speed timings that are associated with the maximum and minimum clock speed settings. There are four speed settings available with the HAL framework, which are as follows:

•   Low

•   Medium

•   Fast

•   Very Fast

I will be using both the Low and Very Fast settings and applying them to signal outputs from pins PC0 and PC1, respectively. No additional MCU hardware is required. However, you will need a fast multi-channel oscilloscope to replicate this demonstration. The oscilloscope should also have a minimum bandwidth rating of at least 100 MHz. I used a Picoscope USB oscilloscope, model 3406B, to capture the measurements. This test device functions with a PC to measure and display up to four independent channels.

## Setting the Pin Clock Speeds

The PC0 and PC1 pin clock speeds are set by creating two more GPIO_InitStruct C data structures and placing them in the `MX_GPIO_Init(void)` method. In addition, there will be a small amount of code required in the `main()` method.

The two new GPIO_InitStruct C data structures are listed below:

![Images](c0125-01.jpg)

![Images](c0126-01.jpg)

The new C structs set up the pins as identical GPIO outputs with the exception that one is low speed and the other is very fast speed. The code segment in `main()` simply toggles the pin outputs between high and low at the fastest possible rate because there is no other intervening code between the output statements.

### Test Results

[Figure 5-13](#ch5.xhtml_ch5fig13) is a screenshot showing an instantaneous capture of the GPIO pin signal waveforms.

![images](fig05-13.jpg)

**Figure 5-13**   *PC0 and PC1 pins’ signal waveforms.*

It is easy to see that the signal waveforms are not crisp digital signals with sharp transitions but instead are slightly distorted with definite rising and falling edge slopes. The distortions are likely due to high oscilloscope probe capacitive loading and the slight inductance due to the jumper leads I connected between the oscilloscope probes and the Arduino protoboard sockets. I also used 10× high impedance probe settings to help reduce the loading on the GPIO pins. I know this helped because I repeated the measurements using the direct X1 probe settings, which further distorted the settings. The vertical voltage amplitude scale must be multiplied by 10 to account for the 10× probe settings.

If you carefully examine the figure you should see two automatic measurements that were computed by the oscilloscope on the displayed waveforms. I have repeated these measurements below for easy viewing:

Pulse period: 94.1 ns

Frequency: 10.62 MHz

I also closely examined waveforms in [Figure 5-13](#ch5.xhtml_ch5fig13) to estimate parameters that I used to calculate the equivalent bandwidth necessary reflecting the measured waveforms leading edges. I also used a rule of thumb for estimating the equivalent bandwidth using the leading edge rise time. These calculations follow:

![Images](c0127-01.jpg)

The 70-MHz bandwidth calculated for the Very Fast speed setting reflects several factors including the maximum possible AHB1 bus speed, which is 100 MHz and the STM32F302R8 high-speed clock rate, which is 72 MHz for the Nucleo-64 development board it controls. All-in-all, a 70-MHz bandwidth is fairly decent while the 19.4 MHz for the Low speed setting could be problematic for demanding applications such as very high-speed data communications. My experimental results actually agree quite closely with STM’s estimates of 75 MHz for the Very Fast setting and 25 MHz for the Low setting.

### Summary

This chapter’s focus was on how to work with GPIO pins and the HAL. I began with a review of how STM peripherals are memory-mapped because that is the fundamental basis on how the MCU configures and controls them.

I next proceeded to discuss how a typical GPIO hardware pin is set up and the various functions by which it may be configured including as an input, an output, an analog role, or an alternate function. The various control registers associated with a GPIO pin were also discussed.

A simple LED test demonstration was next shown where I used an LED/resistor combination, which was inserted into Arduino protoboard sockets. The protoboard in turn was inserted into the Nucleo-64 development board. I went through all the program changes required to be entered into a main.c file in order to light the LED. A complete and annotated main.c listing was provided for your reference and use.

The above program was next modified to accommodate multiple outputs, which controlled an additional LED.

The next demonstration illustrated how the blue user bush button located on the Nucleo-64 development board could be programmed with a GPIO input pin to light an LED when it was pressed. The purpose of this program was to show you how to set up a GPIO pin as an input.

The last demonstration concerned how the GPIO clock speed parameter affected GPIO signal output waveforms. I explained that the clock speed was a misnomer and the real intent was to control GPIO signal skew. Skew is the time it takes to transition from one state to another state.

## 6

## Interrupts

This chapter covers interrupts. As the name implies, they deal with stopping the normal program execution upon recognition of a predesignated event and then attending to that event.

### Interrupts

An interrupt from a high-level perspective is any process that momentarily stops an ongoing program execution and requires the MCU to execute specialized code related to the event that initiated the interrupt. This specialized code is known as an interrupt handler. The event that causes the interrupt is termed an *asynchronous event*, meaning that it has no causal relationship with the normally executing program code. You will shortly see that timer peripherals are typically the source of these asynchronous events. Data communication channels as well as direct memory access (DMA) processes also commonly use interrupts.

An interrupt can originate with hardware, which is the case when a timer is involved. It can also be purely software driven, which will often happen when an abnormal program termination is detected, such as an attempt to divide by zero or attempting to access a nonexistent memory location. Software interrupts in most computer languages are normally referred to as exceptions. However, in ARM terminology, all interrupts whether they are hardware or software initiated are called exceptions.

The ARM Cortex-M integrated peripheral (IP) contains a hardware device called the nested vector interrupt controller (NVIC) whose purpose is to manage exceptions. [Figure 6-1](#ch6.xhtml_ch6fig1) is a block diagram illustrating how the NVIC is connected with other key Cortex-M components, including the Cortex-M core and other peripherals.

![images](fig06-01.jpg)

**Figure 6-1**   *NVIC block diagram.*

You can see two types of wired connections in the left side of [Figure 6-1](#ch6.xhtml_ch6fig1). A single line labeled NMI stands for non-maskable interrupt and is used to allow a peripheral to signal the NVIC to unconditionally start the interrupt process. The other interrupt type is IRQ, which stands for interrupt request. This interrupt type can be masked, meaning that the NVIC does not have to immediately respond to an IRQ if a corresponding masking IRQ register bit has been set. There is usually only one NMI, but there are many IRQ lines that are dependent on the specific model NVIC capacity.

The NVIC is also linked between the Cortex-M core with both dedicated I/O lines and the standard internal bus interconnect structure. This means the NVIC is completely CMCIS compliant and uses the same type of control and configuration registers as has been detailed in the GPIO discussion. The NVIC is fully integrated into the HAL software framework and uses its own C structures to set up a variety of registers. Driver software for the NVIC will be discussed in a demonstration program. At this point, I will discuss some important details regarding the NVIC.

## NVIC Specifications

The STM NVIC general specification states that up to 256 interrupt channels can be managed by a single NVIC. Out of the 256 channels, 240 may be external, while 16 are always internal. In reality, the NVIC portion of the STMF302R8 MCU, which controls the project development board, only supports 52 channels. In addition, there are 16 hardware interrupt lines that have direct connections to the NVIC. Any of the MCU’s 51 GPIO lines may be configured as a maskable interrupt, which means they can become an interrupt channel. You should think of an interrupt channel as more of a software construct than a hardware implementation. In fact, the interrupt C structure uses the word “channel” to reinforce this concept.

Interrupts also may be assigned a priority level. This means that a higher priority interrupt can interrupt a lower priority interrupt. This action gives meaning to the word “nested” in the acronym NVIC. An 8-bit register holds interrupt priority levels, which means there can be a maximum of 256 priority levels. I cannot conceive of a practical embedded system that would ever need anywhere that many interrupt priority levels. Such a system would likely be impossible to design, let alone implement.

It is time to now return to a detailed discussion of the interrupt process as I have already introduced the NVIC.

### Interrupt Process

There a few definitions to be set forth before proceeding with this section:

•   Arm: Allows a hardware device to trigger an interrupt

•   Disarm: Disallows a device to trigger an interrupt

•   Enable: Allows the interrupt process

•   Disable: Disallows the interrupt process

Enabling and disabling interrupts are easily accomplished in the C language by using the `EnableInterrupts()` and `DisableInterrupts()` methods, respectively. A potential interrupt source can trigger an interrupt provided that interrupts are enabled and a specific trigger bit associated with that potential source has been set in the appropriate NVIC control register. This is considered arming a specific device. Conversely, resetting that same register trigger bit will be considered disarming the device. There is one important deviation from this procedure when considering the SysTick interrupt. It has no enable bit because of its importance in having its events always recognized by the MCU.

Interrupt priorities are established by setting appropriate bits in the NVIC BASEPRI register. For example, if a specific interrupt is set at a priority level equal to 3, then any interrupt with priority level of 0, 1, or 2 will interrupt the level 3 interrupt. However, if the BASEPRI register is set to 0, then the interrupt priority feature is disabled and all interrupts are processed as they are received by the NVIC.

There are five preconditions that must be true before an interrupt can be generated:

1.   The potential interrupt device must be armed, that is, trigger bit set.

2.   NVIC must be enabled.

3.   Global interrupts must be enabled.

4.   Interrupt priority must be higher than the current level.

5.   An actual hardware triggering event must happen.

These five conditions can happen in any order. However, they must all be true simultaneously for an interrupt to be recognized and processed.

The following five events will happen if an interrupt is recognized:

1.   The instruction currently executing will complete.

2.   The currently operating thread will be suspended.

3.   The contents of 12 registers will be stored on the stack. An additional 18 words will be stored if the floating point unit (FPU) happened to be active when the interrupt was recognized.

4.   The LR register is set to a specific value. (LR is a special stack register.)

5.   The PC register is loaded with the interrupt service routine (ISR) address.

[Figure 6-2](#ch6.xhtml_ch6fig2) is a graphical depiction of the five events listed above.

![images](fig06-02.jpg)

**Figure 6-2**   *Interrupt processing sequence.*

The key point to make is that the NVIC upon recognizing a valid interrupt request will interface automatically with the MCU using firmware stored within the NVIC. No special code is needed, which makes the interrupt processing as fast as possible. It only takes 12 clock cycles, as shown in [Figure 6-2](#ch6.xhtml_ch6fig2), to go from recognizing an interrupt to executing the first instruction in the ISR. This means there is a latency time of approximately 1.5 µs for an MCU clocked at 80 MHz.

This series of events is called a context switch and is automatically invoked by the NVIC hardware. The result of a context switch is that the currently operating thread becomes a background thread and the ISR becomes a foreground thread. The context switch also works quite nicely with prioritized interrupts where the lower priority ISR becomes a background thread and the higher priority ISR becomes a foreground thread.

There is also the concept of a pending interrupt request, which you should know about. A requesting interrupt is held in a pending state if it is detected if the global interrupts are not yet enabled or the requesting interrupt has a lower priority than a currently active interrupt. Once the five preconditions are met, the requesting interrupt’s state will be changed from pending to active.

It is also very important to clear all device trigger bits or else there will be continuous interrupt requests reoccurring. It is called an acknowledgment to clear a trigger bit and is done by a software instruction. The only device which has an automatic acknowledgment is the SysTick interrupt because of its critical role in MCU operation and its recurring nature of operation. The acknowledgment instruction is almost always included in the ISR.

A few words on the nature of an ISR would be helpful in order to understand what role it plays in the interrupt process. The ISR contains all the code required to process and complete whatever action prompted the initial interrupt. An ISR is usually a very compact software module designed for a single task supporting the interrupting device. However, there is one implementation where just one large ISR services many interrupt sources. In this case, a polling technique is employed to determine the exact interrupt source and use just that portion of the large ISR to service the interrupting device. This is not the case for STM MCUs. The STM implementation uses separate and small ISRs to service each requesting interrupt device. There is a list of addresses for these small ISRs stored in a vector table. This feature gives rise to the word “vector” in the NVIC name.

I do want to mention one area where the STM vectored interrupt process actually uses polling. This would be the case where multiple GPIO pins on the same port could separately issue their own interrupt. Since the GPIO port only has one vector address, it is left to the software to poll all the port’s trigger bits to determine which bit is armed (requested the interrupt).

Every ISR is written to service the interrupting device as efficiently as possible and will issue the acknowledgment as well as invoke the context switch. The latter is easily accomplished by a C language command that has an assembly language format similar to `BX LR`, which will very quickly pop all the stored register values back to their respective registers and thus restore the MCU to its pre-interrupt state. It is software engineering design objective that ISRs should run as quickly as possible and return to the previous foreground thread. This means no wait loops should ever be placed in an ISR.

Any data which is generated or modified in an ISR must be stored in globally shared memory locations, because it will otherwise not be available to any other software module due to the nature of how the C language implements the ISR framework.

## External Interrupts

External interrupts such as those which are sourced through GPIO pins are connected to the NVIC using an external interrupt controller (EXTI). Using an EXTI allows for multiplexing of many GPIO pins into the NVIC external interrupt inputs. [Figure 6-3](#ch6.xhtml_ch6fig3) is a block diagram of the EXTI.

![images](fig06-03.jpg)

**Figure 6-3**   *EXTI block diagram.*

The EXTI controller in the STM32F302R8 MCU carries out the following activities:

•   Handles up to 23 separate software events and/or hardware triggers connected to 16 external interrupt/event lines

•   Provides a status bit for each line

•   Provides independent triggers and masks for each line

•   Can detect external pulse with a shorted clock period than the APB2 bus clock, which drives the EXTI

Any of the STM32F302R8 51 GPIO pins may be used as an interrupt source. Of course, only up to 23 could be active at any given time. That many external interrupts should easily be able to handle any conceivable embedded design. There are also five other EXTI lines that are connected as follows:

1.   EXTI line 16 connected to the PVD output

2.   EXTI line 17 connected to the RTC Alarm event

3.   EXTI line 18 connected to the USB OTG FS Wakeup event

4.   EXTI line 21 connected to the RTC Tamper and TimeStamp events

5.   EXTI line 22 connected to the RTC Wakeup

[Figure 6-4](#ch6.xhtml_ch6fig4) shows relationship between the GPIO pins, external interrupt controller inputs, and the NVIC IRQs.

![images](fig06-04.jpg)

**Figure 6-4**   *GPIO pins, external interrupt controller, and NVIC IRQs.*

You should take note that GPIO pin PC13 is grouped together with many other pins into a common NVIC IRQ named EXTI15_10_IRQ. This is quite important in the interrupt program demonstration.

At this point, you should have gained sufficient knowledge to appreciate a simple interrupt demonstration discussed in the next section.

## Interrupt Demonstration

This interrupt demonstration will be created such that a user can push the blue button on the Nucleo-64 board and cause the user LED to blink at a different interval toggle, that is, push it once to blink twice per second turn and push it again to have it blink once every two seconds. The program takes full advantage of the HAL framework to invoke the appropriate GPIO interrupt for GPIO pin PC13 connected to the blue user push button. The ISR contains code that toggles LD2, a green LED, which is connected to GPIO pin PA5.

The following is a complete code listing for the main.c file contained in the project. A discussion of key parts of the code follows the listing.

![Images](c0137-01.jpg)

![Images](c0138-01.jpg)

![Images](c0139-01.jpg)

![Images](c0140-01.jpg)

![Images](c0141-01.jpg)

Examining the `MX_GPIO_Init` method reveals that it is not much different than the code for the same method used in the previous chapter. The two changes in the method are as follows:

GPIO pin PC13 has been configured to generate an interrupt when pressed by the following statement:

![Images](c0141-02.jpg)

Next, the external interrupt was assigned a priority by the statement:

![Images](c0141-03.jpg)

The NVIC was then enabled to recognize an interrupt from PC13 by the following statement:

![Images](c0141-04.jpg)

That’s all the changes necessary to be applied to the `MX_GPIO_Init` method.

The only thing left is to add the ISR handler code to the project. This ISR must be placed in the stm32f3xx_it.c file. The ISR signature is `void EXTI15_10_IRQHandler(void).` The complete stm32f3xx_it.c file listing is shown below:

![Images](c0142-01.jpg)

![Images](c0143-01.jpg)

You should immediately see that the ISR has only seven statements, which agrees very nicely with my earlier discussion that ISRs must be as concise as possible and dedicated to a single task. The first statement is a no operation (nop) “for” loop that introduces a very short delay to debounce the push button. The next statement is a compound “if” that reads the voltage level connected to the push button. It will be high because the program is already in the interrupt handler. If the external C variable tDelay is set to 250, it will be reset to 1000 and vice versa. The last statement in the ISR activates the NVIC IRQ handler for the external controller connected to pin PC13.

### Test Run

I built the project and downloaded that into the Nucleo-64 board using the procedure detailed multiple time in previous chapters. I initially observed that the LED blinked twice a second after the initial download. I then pressed the blue button and observed that the LED started blinking at a rate of once every two seconds. Pressing it again returned to the twice a second blink rate. This was a convincing proof that the interrupt demonstration was working as desired. Admittedly, this is a very simple demonstration, yet it contains all the elements necessary to support far more complex interrupt driven programs. You find that interrupts are an embedded developer’s best friend. Most of my embedded development projects use interrupts. Not using them deprives you of an important tool in creating efficient embedded programs. It is not an overstatement to say that modern embedded projects would not be practical without employing at least one interrupt.

### Summary

I started the chapter by discussing how the STM MCU interrupt process functions. This discussion included the description and functioning of the NVIC and a walk through a complete interrupt processing sequence.

An interrupt demonstration next followed in which a user pressed the blue push button located on the project Nucleo-64 board, which caused an interrupt to be generated. The corresponding interrupt service routine (ISR) code consequently toggled the state of an onboard LED.

## 7

## Timers

Timer peripherals are very important components within a MCU. Many embedded applications are time or temporal dependent and timers are the primary means by which the MCU controls the application. While it is certainly possible to use a MCU to directly time processes, it would be great waste of processing power and highly inefficient approach. Using hardware timers along with interrupts is really the only practical way to implement embedded time-dependent applications. Fortunately, there is a powerful timer variety provided by STM in its line of MCUs.

### STM Timer Peripherals

A timer is simply a free-running counter that counts pulses from a clock source. Since the pulse train from a clock source has a known period or interval between pulses, the elapsed time is directly related to the number of pulses counted. The timer clock source used with a typical MCU is usually derived from an internal master clock. However, the master clock usually runs at a very fast speed, so timer pulses must be divided by hardware to more reasonable values that can be used by timers. The hardware used to “slow” the master clock rate varies and can be binary dividers (prescaler) or phase-locked loops (PLL). Timer counters can count up or accumulate counts until they overflow based on the number of bits used in the counter. A 16-bit counter will overflow when the maximum count of 65535 is reached. An overflow interrupt is often the event which happens with this situation.

Conversely, a timer counter can count down from some preset value and trigger an interrupt when it reaches a 0 value. This counter type is known as a decrementing counter and has many uses.

Timers have many uses, including but not limited to the following:

•   Generating a precise time base. All STM timers can do this.

•   Measuring the frequency of an incoming digital pulse train.

•   Measuring elapsed time on an output signal. This is called output compare for STM timers.

•   Generating precise pulse-width modulation (PWM) signals used for servo and motor control.

•   Generating single pulse with programmable length and delay characteristics.

•   Generating periodic direct memory access (DMA) signals in response to update, trigger, input capture, and output compare events.

There are following five broad categories of STM timers:

•   Basic: Simple 16-bit timers. They do not have inputs or output pins. They are principally used as “masters” for other timers. They also are used as a digital-to-analog converter (DAC) clock source. They can generate a time base like all STM timers can do.

•   General purpose (GP): These are 16-bit or 32-bit timers with both input and output pins. They can do all of the functions described in the above list. GP timers can have up to four programmable channels, which may be configured as follows:

•   One or two channels

•   One or two channels with a complementary output. The complementary output has a “dead time” generator, which provides for an independent time base.

•   Advanced: All the features of the GP timer with additional functions related to motor control and digital power conversion. There are three complementary outputs available with this timer category with an emergency shutdown input.

•   High resolution: Multiple high-resolution outputs made possible by six sub-timers, one master and five slaves. Multiple dead-time insertions are possible with this timer. There are also five fault inputs and 10 external event inputs. This timer has the acronym HRTIM1 in STM terminology.

•   Low power: Timers used in exceptional low-power applications. These timers are designed to stay running in just about all STM MCU modes, except the Standby mode. They can even continue to operate without an internal clock source.

The STM32F302R8 MCU used in the demonstration board has basic, GP, and advanced timers. I will focus on how these timers function and are programmed. The concepts discussed will also apply to the other timer types if you encounter them in other projects. As always, the manufacturer datasheets are your best resource to determine how a particular timer works and how it should be programmed.

The STM32F302R8 MCU has six timers, as shown in [Table 6-1](#ch7.xhtml_ch6tab1). This table has a handy reference to keep in mind when selecting and programming a timer.

![images](tab06-01.jpg)

**Table 6-1**   *STM32F302R8 MCU Timers*

I will now discuss how to configure a STM timer using the HAL framework.

### STM Timer Configuration

STM timers are configured in the same manner as GPIO pins and interrupts as I have previously discussed. STM timers are configured with a C structure named `TIM_HandleTypeDef`, which contains the following members:

![Images](c0147-01.jpg)

![Images](c0147-02.jpg)

The struct members represent the following timer parameters and settings:

•   Prescaler: The division factor used to scale the master clock rate. There are only 16-bit prescalers used in all the timers. A 16-bit register can hold prescaler values ranging from 1 to 65535\. For example, a prescaler value of 40,000 applied to an 80-MHz master clock would mean a 2-kHz clock rate would be input into the timer.

•   CounterMode: Sets the count direction. The available CounterModes are as follows:

•   TIM_COUNTERMODE_UP

•   TIM_COUNTERMODE_DOWN

•   TIM_COUNTERMODE_CENTERALIGNED1

•   TIM_COUNTERMODE_CENTERALIGNED2

•   TIM_COUNTERMODE_CENTERALIGNED3

•   Period: This is a number that represents the maximum time to be elapsed before the timer counter is reloaded with this number. The maximum number is 0xffff for 16-bit counters and 0xffff ffff for 32-bit counters. A value of 0x0 will ensure a timer does not start.

•   ClockDivision: This is a bit-specific field used for setting the ratio between the internal timer clock frequency and a sampling clock used for digital filters. It is also used to set dead-time parameters. The available ClockDivision modes are as follows:

•   TIM_CLOCKDIVISION_DIV1

•   TIM_CLOCKDIVISION_DIV2

•   TIM_CLOCKDIVISION_DIV4

•   RepetitionCounter: Sets a limit for the number of times a timer can overflow or underflow. The timer update register will be set when the limit is reached. An event can also be raised in conjunction with the register update.

## Update Event Calculation

The following equation should be used to compute the time between update events for a given high-speed clock rate, a prescalar value, and a period value:

![Images](c0148-1.jpg)

A sample calculation is shown below:

Given:

![Images](c0149-01.jpg)

The discussion on the demonstration project presented below will show you how to configure a GP timer in a polled mode, which in turn will blink an LED.

### Polled or Non-interrupt Blink LED Timer Demonstration

This is the first of two demonstrations showing you how to configure the TIM2 GP timer to control LD2, the onboard green LED. This demonstration will not use an interrupt, so I can focus on the discussion of how to configure a timer. The LED will blink at a 0.5-s rate based on the selection of prescaler and period values as well as the Nucleo-64 board’s preset 64-MHz high-speed clock rate.

You should start this project using the CubeMX application by providing an appropriate project name. I used the name TIM2_Example1 for this project. In the Pinout view, you should select the internal high-speed clock as timer TIM2 clock source, which is shown in [Figure 7-1](#ch7.xhtml_ch7fig1).

![images](fig07-01.jpg)

**Figure 7-1**   *TIM2 clock source selection.*

Selecting the clock source also triggers the CubeMX application to include all the TIM2 initialization statements to be included in the new project. This step is vital to generate a working project.

Don’t forget that all the other previous project creation steps are still appropriate, such as including only the necessary library files and ensuring that a hex file is generated.

I will discuss the key parts of the project code after the below listing.

![Images](c0150-01.jpg)

![Images](c0151-01.jpg)

![Images](c0152-01.jpg)

![Images](c0153-01.jpg)

![Images](c0154-01.jpg)

Most of this code is a repeat of the main.c code shown in the interrupt demonstration project discussed in the previous chapter. The key differences are the addition of a `MX_GPIO_Init` method and some new operational code required in the forever loop portion of the `main` method.

The `MX_GPIO_Init` method configures the `TIM_HandleTypeDef,` a typed C struct with specific values to have the timer reset every 0.5 s. The struct is named htim2 and is both initialized and started in this method.

The forever loop in the `main` method has code, which continually checks the timer count and will turn on the LED when the count reaches 150\. It will remain on until the count progresses to a value of 399, at which point the LED will be reset. These statements result in the LED being on for 0.25 s and off for 0.25 s.

## Test Run

I built the project and uploaded it into the Nucleo-64 board. The user LED immediately began to blink at a 0.5-s rate, which confirmed the program worked as desired. The next step in this timer demonstration series is to implement an interrupt-driven version that will also blink the LED, but not require any specialized code in the `main` method’s forever loop.

### Interrupt-Driven Blink LED Timer Demonstration

This demonstration will also blink an LED. In this demonstration, I will use an interrupt approach, thus eliminating any specialized code in the forever loop main that continually reads the timer counter value and reacts when certain values are reached.

You will need to generate a new project using the CubeMX application. I named this project Timer_int to reflect its purpose. You will also need to select the timer clock source as has been done in the previous demonstration. Simply use the internal high-speed clock as the source, which will trigger the application to include all the TIM2 timer initialization and configuration code. However, this time you will also have to set up the timer to trigger an interrupt when its period is elapsed. This is easily done using the CubeMX Configuration tab. You should see timer TIM2 appear in the tab, but first ensure you have selected the clock source. Otherwise timer TIM2 will not appear. Click on the TIM2 icon and then click on the enable global interrupt check box. The Configuration tab and the enable global interrupt check box are both shown in [Figure 7-2](#ch7.xhtml_ch7fig2).

![images](fig07-02.jpg)

**Figure 7-2**   *Configuring timer TIM2 interrupt functionality.*

I will not repeat the extensive code listing previously shown, but will instead just present the code segments needed to implement the interrupt-based code.

The first part is the easy one, where the forever loop is changed to a null action:

`while(1);`

The only other change that needs to be done is to set the timer period to 250 to ensure the LED blinks twice a second. The timer will now interrupt at the appropriate interval without any special code needed to monitor real-time counter values.

The following three statements must be added just before the forever loop in the `main` method:

![Images](c0156-01.jpg)

The TIM2 IRQ handler method must be defined in the main.c file as follows:

![Images](c0156-02.jpg)

Finally, a callback method must also be defined, which toggles the LED pin every time the TIM2 timer generates an interrupt:

![Images](c0156-03.jpg)

![Images](c0157-01.jpg)

## Test Run

I made the modifications to the main.c file, built the project and then uploaded it into the Nucleo-64 board. The user LED immediately began to blink at a 0.5 second rate, which confirmed the program worked as desired.

### Multi-rate Interrupt-Driven Blink LED Timer Demonstration

This demonstration is an expansion of the previous demonstration in which the user LED will be repeatedly blinked at two different rates, one at 0.5 s and the other at a 1.0-s rate. A timer interrupt will also be used in this program but with a significant difference between the single- and multi-rate implementations. In the single-rate program, the LED is directly controlled in the callback function. In the multi-rate version, the callback function simply increments a counter variable, which is then used in the forever loop to control the LED. The incrementing counter variable `timCnt` causes the LED to be set or reset depending on its value. The following listing is the complete main.c listing. I have also added additional comments regarding the forever loop code snippet following the listing.

![Images](c0157-02.jpg)

![Images](c0158-01.jpg)

![Images](c0159-01.jpg)

![Images](c0160-01.jpg)

![Images](c0161-01.jpg)

![Images](c0162-01.jpg)

![Images](c0163-01.jpg)

The forever loop contains a series of if statements that will be triggered based on specific counter values. The statements within the if statements either set or reset the user LED. Each counter increment takes 0.25 s to complete, which means that two increments will take 0.5 s. The LED will toggle at two times per second for the first 4 s. The second set of 4 s will toggle the LED once every second.

This code format is rather lengthy, but it does trade code space for simplicity. It is rather easy to follow the algorithm step-by-step to determine how the LED is controlled using this format.

![Images](c0163-02.jpg)

![Images](c0164-01.jpg)

## Test Run

I built the project and then uploaded it into the Nucleo-64 board. The user LED immediately began to blink at a 0.5-s rate for 4 s and then at a 1.0-s rate for 4 s, which confirmed that the program worked as desired.

### Modification to the Multi-rate Program

I changed code snippet in the above forever code to make that much more compact. That modification is listed below.

![Images](c0165-01.jpg)

The program functioned just about the same with this modified code, which used the modulus operator along with a toggle method to control the LED. The code is much smaller than the original, but it is more complex and harder to understand and consequently maintain. This change highlights an interesting challenge that developers constantly face. This challenge is whether or not to use simpler code, which can take more code space versus using compact and “efficient” code, which is likely harder to understand and modify.

## Test Run

I built the modified project and then uploaded it into the Nucleo-64 board. The user LED immediately began to blink at a 0.5-s rate for 4 s and then at a 1.0-s rate for 4 s, which confirmed the modified program worked the same as the original program. I did notice that the LED seemed to flicker more using this version vice the original. I can only attribute the flicker to the use of the toggle method versus the firm set and reset methods.

This last demonstration completes all discussions and demonstrations that I wished to convey regarding interrupts and timers. This chapter really is just the tip of the proverbial iceberg because there is a tremendous amount of information on these topics that I could not cover. There are almost 2,000 pages alone in STM’s HAL user manual. As always, the STM datasheets, and user and reference manuals will be an invaluable resource to learn about the many additional features and functions that you can carry out with interrupts and timers.

### Summary

I started the chapter discussions with the focus on timers, which are important peripherals because they alleviate the MCU from having to directly perform timing functions. I explained the five available categories of STM timers, of which there are three types provided on the project MCU. These are basic, general purpose (GP), and advanced.

I next showed you how to configure a timer to perform a specific timing event. This discussion was followed by a demonstration in which the onboard LED blinked once per second. This demonstration did not use an interrupt, which was the focus of the second timer demonstration.

In the second timer demonstration, I showed how easy it was to integrate a timing operation with an interrupt process. In this demonstration also the onboard LED blinked, but it blinked using only the interrupt process.

The third timer demonstration showed how to restructure the interrupt process such that a multi-rate LED blink could be implemented. The interrupt callback method controlled a counter variable, which in turn controlled the actual LED activation within the forever loop.

In the final timer demonstration, I changed the original forever loop code with a much more compact and complex version with the same functionality . I did this to illustrate how developers must constantly decide on how to write code, simpler and consuming more code space or very compact and complex, which is harder to understand.

## 8

## Bit Serial Communications

This chapter covers how a MCU uses bit serial communication to bidirectionally transfer data between it and external devices and systems. The primary peripheral devices used for this function are the universal asynchronous receiver transmitter (UART) and the universal synchronous/asynchronous receiver/transmitter (USART). The principal difference between these peripherals is that the USART can use a synchronizing clock pulse train between nodes, while the UART is completely self-synchronizing. These differences are explained in more detail in the following section “UARTs and USARTs.”

### UARTs and USARTs

[Figure 8-1](#ch8.xhtml_ch8fig1) is a block diagram showing two UARTs connected, where Node A is transmitting to Node B.

![images](fig08-01.jpg)

**Figure 8-1**   *UART block diagram.*

The digital pulse train between the nodes is composed of one start bit, eight data bits, and one stop bit. These bits all together are considered to be a single frame. You should note that the start and stop bits are 50% longer in duration then the data bits. This difference in pulse duration is how the UART distinguishes the start and stop bits from the data bits. The receiving node must detect the start bit in order to determine when the frame starts. The receiving node also has been configured to accept a predetermined number of data bits and whether or not there will be one or two stop bits. UARTs can be set to send seven or eight data bits as well as one or two stop bits. There is also a provision for sending an additional parity bit, which aids in detecting transmission errors. Often, parity bits are not used, especially in cases where the transmission channel is not noisy or transmission line delays are not present.

The USART is a variant of the UART because an additional clock line can be used between nodes, as shown in [Figure 8-2](#ch8.xhtml_ch8fig2).

![images](fig08-02.jpg)

**Figure 8-2**   *USART block diagram.*

There is no need for start and stop bits to be used when two USART nodes are interconnected, as shown in [Figure 8-2](#ch8.xhtml_ch8fig2). The data bits are clearly synchronized to the clock pulses, which shortens the frame length and improves channel communication efficiency. However, seven or eight data bits may be set as well as a parity bit, as was the case for the UART node. It should also be obvious from the name that a USART can operate as a UART, if so desired.

[Figure 8-3](#ch8.xhtml_ch8fig3) is a block diagram that shows full-duplex communication setups using UART and USART nodes.

![images](fig08-03.jpg)

**Figure 8-3**   *Full-duplex communications block diagram.*

Full-duplex communications means that data can simultaneously be sent and received between nodes. This is strictly possible because each node’s UART or USART is controlled by its own MCU.

Often, it is important to assess the state of a given node that it is able to actively participate in a communications link. It can happen that a receiving node’s MCU is temporarily blocked for some reason and while a remote node’s UART can send data, the receiving node may not be able to process it. For this reason, there are protocol control lines that are provided in UART and USART hardware to ensure that data is sent and received when allowed. The two primary control lines are request-to-send (RTS) and clear-to-send (CTS). A node that desires to transmit data would first raise or set the RTS line. The receiving node would then raise or set the CTS line indicating that it is okay to send the data. This process is also known as request/acknowledge and is commonly used in full-duplex communications links. However, this protocol is really not required for the book projects because the project board MCU will never be blocked and the receiving node will typically be a PC, which will also never be blocked.

There are two USARTs in the STM32F302R8 MCU use in the project board. These are logically referred to as USART1 and USART2\. They are the primary means by which the MCU can send and receive data other than by processing data bits through the GPIO ports or by using one of the other communication protocols, such as the I2C and SPI bit-serial interfaces. The latter two are used mainly for sensor data, although there is a very nice I2C peripheral that can display text messages. Later in the chapter, I will discuss how to set up the USART2 USART to communicate with a PC terminal program. However, I now need to discuss how to initially configure a USART.

***NOTE***  *The software to initialize and configure UARTs and USARTs is identical. Do not worry that a USART is being discussed, while the function or typedef has UART in the name.*

## USART Configuration

STM USARTs are configured in a similar manner as GPIO pins, interrupts, and timers that I have previously discussed. STM USARTs are initialized using a C struct named `UART_HandleTypeDef.` It is configured using a C struct named `UART_InitTypeDef`. I will first discuss the `UART_HandleTypeDef`, which contains the following members:

![Images](c0170-04.jpg)

Some of the more important members of this struct are discussed below:

•   Instance: This is the pointer to the USART descriptor. For example, USART2 is the descriptor of the UART associated to the ST-LINK interface.

•   Init: This is an instance of the C struct UART_InitTypeDef, which is used to configure the UART interface.

•   AdvancedInit: Used to configure more advanced UART features like the automatic BaudRate detection and TX/RX pin swaps.

•   pTxBuffPtr: Points to the transmit buffer used as the data source for transmitted bytes.

•   TxXferCount: Holds the count of transmitted bytes.

•   pRxBuffPtr: Points to the receive buffer where incoming bytes will be stored.

•   RxXferCount: Holds the count of received bytes.

•   Lock: This field is used internally by the HAL to lock concurrent accesses to UART interfaces.

The C struct `UART_InitTypeDef` contains the following members:

![Images](c0171-02.jpg)

These struct members represent the following USART parameters and settings:

Baudrate: This parameter is the connection speed in bits per second. [Table 8-1](#ch8.xhtml_ch8tab1) shows a chart of standard and nonstandard baud rates that are available with the STM USART peripheral.

![images](tab08-01.jpg)

**Table 8-1**   *Baud Rate Chart*

•   WordLength: This value specifies the number of data bits transmitted or received in a frame. This field can assume one of the following defines:

•   UART_WORDLENGTH_8B

•   UART_WORDLENGTH_9B

•   StopBits: This field specifies the number of stop bits transmitted. This field can assume one of the following defines:

•   UART_STOPBITS_1

•   UART_STOPBITS_2

•   Parity: This value indicates the parity mode. This field can assume one of the following defines:

•   UART_PARITY_NONE

•   UART_PARITY_EVEN

•   UART_PARITY_ODD

•   Mode: This value specifies whether the RX and/or TX mode is enabled or disabled. This field can assume one of the following defines:

•   UART_MODE_RX

•   UART_MODE_TX

•   UART_MODE_TX_RX

•   HwFlowCtl :This value specifies whether the RS2326 Hardware Flow Control mode is enabled or disabled. This field can assume one of the following defines:

•   UART_HWCONTROL_NONE

•   UART_HWCONTROL_RTS

•   UART_HWCONTROL_CTS

•   UART_HWCONTROL_RTS_CTS

OverSampling: This value helps discriminate noise from true signal levels. The selected oversampling rate is a tradeoff between noise immunity and maximum possible communication speed. This field can assume one of the following defines:

•   UART_OVERSAMPLING_8

•   UART_OVERSAMPLING_16

The above discussion details how a USART can be initialized and configured, but I still need to explain how to set up a communication link between the project board and a remote node, which will be the PC connected to the board.

## Windows Terminal Program

You will need a terminal program installed in order to display the text messages being transmitted from the demonstration board. There are a number of terminal programs that are free and readily available to download. I chose a program named Realterm that is available from [https://sourceforge.net/projects/realterm/](https://sourceforge.net/projects/realterm/). It is full-featured terminal program that I found very easy to configure and run. [Figure 8-4](#ch8.xhtml_ch8fig4) shows the Realterm screen after I clicked on the Port tab.

![images](fig08-04.jpg)

**Figure 8-4**   *Realterm Port screen.*

Note that I selected the following parameters to match those configured in the STM program:

•   Baud—9600

•   Parity— None

•   Data Bits—8

•   Stop Bits—1

•   Hardware Flow Control—None

•   Port—6

The last parameter named Port deserves some further explanation. This value refers to the virtual com port number that was created when I installed the ST-LINK Virtual COM Port USB driver into the host computer. In Windows 10, I had to use the following lengthy sequence just to find the port number:

Control Panel → Hardware and Sound → Devices and Printers → Device Manager → Ports (COM & LPT)

[Figure 8-5](#ch8.xhtml_ch8fig5) shows the screen that appeared when I clicked on the Ports (COM & LPT) selection.

![images](fig08-05.jpg)

**Figure 8-5**   *Ports screen.*

The USART2 peripheral is connected to the ST-LINK circuit, as shown in the [Figure 8-6](#ch8.xhtml_ch8fig6) schematic.

![images](fig08-06.jpg)

**Figure 8-6**   *USART2 connection to ST-LINK schematic.*

GPIO pins PA2 and PA3 are connected as USART_TX and USART_RX, respectively. It is also possible to use these pins as an external USART by shorting the solder bridges SB62 and SB63\. The pins would then be available on both the Arduino and Morpho connectors, as discussed in a previous chapter.

The Realterm program will be all set to display the USART output when the program is run. However, there is an additional step that is required for the USART to work as desired. This is described in the next section.

## Enabling USART2

Up until this program, I have not had to use the IP tree pane view in the CubeMX application to configure a peripheral. That has been done for me by the application because I was only using GPIO pins for a program and not any alternative functions. However, I will now need to enable the USART2 alternative function in order to have the communications link work. You configure USART2 when creating a new project, and the Pinout window is shown. [Figure 8-7](#ch8.xhtml_ch8fig7) shows how USART2 is configured by selecting Asynchronous from the Mode dropdown menu.

![images](fig08-07.jpg)

**Figure 8-7**   *Configuring USART2.*

The CubeMX application will automatically insert an initialization method `static void MX_USART2_UART_Init(void)` in the main.c file when the USART2 function is enabled.

You need to set the appropriate communications parameters in this method as shown in the following code snippet:

![Images](c0176-01.jpg)

At this point, all the prerequisites have been introduced that are needed for an actual USART demonstration program.

### USART Transmit Demonstration Program

The following program will display a continuously varying value in a terminal window. The purpose of this demonstration is to show how the USART can transmit data to a terminal program.

![Images](c0176-02.jpg)

![Images](c0177-01.jpg)

![Images](c0178-01.jpg)

![Images](c0179-01.jpg)

![Images](c0180-01.jpg)

A small amount of functional code has been placed in the forever loop. The following code snippet shows this code with an explanation following the listing.

![Images](c0180-02.jpg)

The `sprintf` statement causes the double variable `value` to be converted to a string with a carriage return and line feed concatenated to the value. The next statement `HAL_UART_Transmit(&huart2, (uint8_t*) msg, 10, 100);` performs the actual transmission of the data from the MCU to the terminal program. The four arguments are as follow:

![Images](c0181-04.jpg)

The next statement `HAL_Delay(200);` introduces a short delay between displaying the value string. The last statement just slightly changes the `value` variable to help with the display.

## Test Run

The program was then built and downloaded into the project board. I then started the Realterm terminal program to display the communication stream from the board. [Figure 8-8](#ch8.xhtml_ch8fig8) shows the terminal output for the UART transmit program.

![images](fig08-08.jpg)

**Figure 8-8**   *Terminal output for the UART transmit program.*

This program will also be used as a template for other book projects that only need a terminal output.

### USART Receive Demonstration Program

The following program will accept alphanumeric characters from a terminal program and will also display those characters. It will also detect a specific character sequence and light the user LED once it is detected. The purpose of this demonstration is to show how the USART can both receive and transmit data to/from a terminal program.

Because any received character will also trigger an interrupt, it is critical that the USART2 global interrupt should be enabled. This is done by clicking on the USART2 icon in the Configuration tab of the CubeMX program. Please follow the same procedure that was used in the timer interrupt example except you will be activating the USART2 global interrupt instead of the TIM2 timer interrupt. Enabling the USART2 interrupt will also cause the CubeMX application to automatically generate the associated callback function where all the required interrupt handling statements will be placed. All received characters are added to a data buffer within the callback function.

![Images](c0182-01.jpg)

![Images](c0183-01.jpg)

![Images](c0184-01.jpg)

![Images](c0185-01.jpg)

![Images](c0186-01.jpg)

![Images](c0187-01.jpg)

## Test Run

The program was then built and downloaded into the project board. I then started the Realterm terminal program to display the communication stream from the board. [Figure 8-9](#ch8.xhtml_ch8fig9) shows the terminal output for the UART receive/transmit program.

![images](fig08-09.jpg)

**Figure 8-9**   *Terminal output for the UART receive/transmit program.*

I did note that the user LED did light when the phrase “LD2 on” was entered. The LED went off when the next character was entered as was expected.

This program will also be used as a template for other book projects that need both terminal input and output.

### Summary

I began the chapter with an explanation of both the universal asynchronous receiver transmitter (UART) and the universal synchronous/asynchronous receiver/transmitter (USART) internal peripherals. This discussion also included how the data transfer protocol worked.

A discussion on how to configure a USART followed. The configuration procedure used two C structs to configure and initialize the USART. I also explained all the elements in both C structs.

I next showed how to install a terminal program, which is required to display alphanumeric data sent out by the USART. I selected the open-source terminal program named Realterm.

An explanation followed on how to enable the USART2 peripheral using the CubeMX application. The USART2 selection was configured in the CubeMX tree pane view. I also went through the procedure on how to configure the device using the C struct.

A demonstration program was next shown, which displayed a numeric variable that was continuously being updated.

The final demonstration displayed manually entered terminal data as well as lighting an LED when a trigger phrase was entered.

## 9

## Analog-to-Digital Conversion

This chapter covers a very important topic of analog-to-digital conversion. The devices that actually do the conversions are called analog-to-digital converters (ADCs). The STM line of MCU has a good variety of ADCs; however, they all operate and are programmed in a similar manner. There is a single ADC used in the project board STM32F302R8 MCU. However, it can accept analog inputs from any 1 of 15 separate external lines. There is a sixteenth ADC input, but it is permanently connected to an internal temperature sensor and is not available for any other use.

Beginners in the embedded development sometimes question the need for an ADC peripheral. The answer is that measurements in the real world are taken typically using analog sensors that provide a continuous range of voltages that are proportional to the environmental parameter that is being monitored. For instance, the Analog Devices TMP36 temperature sensor, shown in [Figure 9-1](#ch9.xhtml_ch9fig1), provides a range of voltages from approximately 0.1 to 2.0 V that is directly proportional to a range of temperatures roughly from –40°C to 150°C. This analog voltage must be converted to an equivalent digital number before being able to be processed by the MCU. That is the role of an ADC.

![images](fig09-01.jpg)

**Figure 9-1**   *Analog Devices TMP36 temperature sensor.*

The following discussion provides a detailed explanation of how a STM ADC functions.

### ADC Functions

The technique used in STM ADCs is known as successive–approximation register (SAR). The architecture for a SAR ADC is fairly simple as may be seen in the block diagram, as shown in [Figure 9-2](#ch9.xhtml_ch9fig2).

![images](fig09-02.jpg)

**Figure 9-2**   *SAR ADC block diagram.*

An analog voltage is first inputted to a track/hold circuit. This circuit is also commonly called a sample/hold circuit, which takes an instantaneous sample of the varying analog voltage and uses that sample as the value to be converted into a digital number. The N-BIT REGISTER block, shown in [Figure 9-2](#ch9.xhtml_ch9fig2), is set at a mid-scale value. This value depends upon the number of bits created in the final conversion. For this discussion, I will use only 4 bits for the conversion, which will be adequate to explain the conversion process. In reality, the real STM ADC uses 12 bits. Getting back to the register will mean a mid-scale value of 1000 will be preset in the register. This value will therefore force the digital-to-analog converter (DAC) shown in the figure as N-BIT DAC to output a voltage equal to V[REF]/2\. V[REF] is a reference voltage used by the ADC and is often the same as the supply or power rail voltage. That would be 3.3 V for most STM MCUs.

A comparison between the sampled analog voltage held by the TRACK/HOLD (V[IN]) module and the DAC output (V[DAC]) is then accomplished by a COMPARATOR module shown in the upper right-hand portion of [Figure 9-2](#ch9.xhtml_ch9fig2). The COMPARATOR will output a 1 if V[IN] is greater than V[DAC], otherwise it will output a 0\. If a 1 is output, the most significant bit in the N-BIT REGISTER will be retained, otherwise it will be reset to 0.

The SAR LOGIC module will then shift 1 bit to the right and repeat the comparison process. This sequence is repeated until the least significant bit (LSB) position is reached and processed. Once that point has been done, the N-BIT REGISTER will then contain the complete digital equivalent to the sampled analog input voltage. The SAR LOGIC module will then allow the fully converted digital value to be released either in a parallel or serial format.

[Figure 9-3](#ch9.xhtml_ch9fig3) shows a complete 4-bit conversion sequence.

![images](fig09-03.jpg)

**Figure 9-3**   *Four-bit conversion sequence.*

The vertical axis represents the V[DAC] voltage and the horizontal axis represents time. The result of the first conversion is to set the MSB to 0 because V[IN] is less than V[REF]/2\. The SAR LOGIC module will then reset the V[DAC] to V[REF]/4 before the next comparison. In this case, V[IN] is greater than V[REF]/4 and the bit one position to the right of the MSB will be set to 1\. Next, the SAR LOGIC module will split the difference between V[REF]/2 and V[REF]/4, which is 3V[REF]/8\. This new comparison results in a 0 being output from the COMPARATOR module. In actuality, the SAR LOGIC module changes the VDAC voltage in some multiple of V[REF]/2⁴ or V[REF]/16 for each comparison operation. This results in the converging step-like waveform, as shown in [Figure 9-3](#ch9.xhtml_ch9fig3). Some multiples of the step value are either added to or subtracted from V[DAC] depending upon the result of the previous bit comparison. In this case the resulting digital value held by the N-BIT REGISTER is 0101, which is 5 in a decimal format. This all makes sense if you equate V[REF] to 16 where each step in the V[REF] range is 1\. The V[IN] line in the figure would then be approximately at the 5 level.

I believe you can see that the SAR process converges fairly rapidly to a final value. In this case, it took four comparisons, while a 12-bit ADC would take 12 comparisons. The good news is the SAR LOGIC module operations are all done in firmware with no MCU instructions required other than to start the conversion.

## ADC Module with HAL

The HAL framework uses a similar C struct to declare ADC peripherals, as has been noted earlier when discussing GPIO pins and timer peripherals. The following C struct is defined for an ADC. Each struct member will separately be discussed after the struct definition.

![Images](c0192-01.jpg)

![Images](c0193-01.jpg)

![Images](c0193-02.jpg)

![Images](c0194-01.jpg)

The `ADC_InitTypeDef` struct members are defined in the following list:

`uint32_t ClockPrescaler;`—This defines the ADC clock speed (ADCCLK) used in the ADC. This clock rate indirectly sets the maximum sample rate possible with the ADC. The ADC prescaler has preset divider rates starting at one and progressing at multiples of 2, that is, 2, 4, 6, or 8\. The ADC clock rate affects all MCU ADCs. This parameter can be any value of the following ADC_ClockPrescaler defines:

![Images](c0194-04.jpg)

`uint32_t Resolution;`—This value sets the ADC resolution. This parameter can be any value of the following ADC_Resolution defines:

![Images](c0194-06.jpg)

There is a definite relationship between the resolution and maximum possible conversions that can be accomplished per second. This rule is *the greater the resolution, the lower the maximum conversion rate*.

`uint32_t DataAlign;`—This value establishes how the bits in the N-Bit register are aligned. This parameter can be any value of the following ADC_DATAALIGN defines:

![Images](c0194-08.jpg)

`uint32_t ScanConvMode;`—This value specifies the ADC mode. It is either single or continuous. This parameter can be either value of the following ADC_SCAN defines:

![Images](c0194-10.jpg)

`uint32_t EOCSelection;`—This value sets the flag type indicating an end of a conversion (EOC). The flag type value also depends upon the ADC mode, which may be single or continuous. This parameter can be set to either of the following ADC_EOC defines:

![Images](c0195-02.jpg)

`uint32_t ContinuousConvMode`—Specifies whether the conversion is performed in single mode (one conversion) or continuous mode for regular group, after the selected trigger occurred (software start or external trigger). This parameter can be set to `ENABLE` or `DISABLE`.

`uint32_t NbrOfConversion;`—This value specifies the number of ranks or channels that will be converted within the regular group sequencer. To use regular group sequencer and convert several ranks, parameter ‘ScanConvMode’ must be enabled. This parameter must be a number between Min_Data = 1 and Max_Data = 16.

`uint32_t DiscontinuousConvMode;`—This value specifies whether the conversion sequence of regular group is performed in Complete sequence/Discontinuous sequence (main sequence subdivided in successive parts). Discontinuous mode is used only if sequencer is enabled (parameter ‘ScanConvMode’). If sequencer is disabled, this parameter is discarded. Discontinuous mode can be enabled only if continuous mode is disabled. If continuous mode is enabled, this parameter setting is discarded. This parameter can be set to `ENABLE` or `DISABLE`.

`uint32_t NbrOfDiscConversion;`—This value specifies the number of discontinuous conversions in which the main sequence of regular group (parameter NbrOfConversion) will be subdivided. If parameter ‘DiscontinuousConvMode’ is disabled, this parameter is discarded. This parameter must be a number between Min_Data = 1 and Max_Data = 8.

`uint32_t ExternalTrigConv;`—This value selects the external event used to trigger the conversion start of regular group. If set to ADC_SOFTWARE_START, external triggers are disabled. If set to external trigger source, triggering is on event-rising edge by default. This parameter can be a value in the format of ADC_External_trigger_Source_Regular and is one of the following defines:

![Images](c0196-01.jpg)

`uint32_t ExternalTrigConvEdge;`—This value selects the external trigger edge of regular group. If trigger is set to ADC_SOFTWARE_START, this parameter is discarded. This parameter can be a value in the format of ADC_External_trigger_edge_Regular and is one of the following defines:

![Images](c0196-03.jpg)

`uint32_t DMAContinuousRequests;`—This value specifies whether the DMA requests are performed in one shot mode (DMA transfer stop when number of conversions is reached) or in continuous mode (DMA transfer unlimited, whatever number of conversions). Note: In continuous mode, DMA must be configured in circular mode. Otherwise, an overrun will be triggered when DMA buffer maximum pointer is reached. Note: This parameter must be modified when no conversion is ongoing on both regular and injected groups (ADC disabled, or ADC enabled without continuous mode or external trigger that could launch a conversion). This parameter can be set to ENABLE or DISABLE.

Don’t be too discouraged by the extent of the above listings. The actual declaration and configuration of a STM ADC peripheral is straightforward and reasonably easy to understand as you will shortly realize by examining a demonstration. However, I still need to cover some remaining ADC topics before proceeding to a real demonstration.

## ADC Conversion Modes

There are few common ways to use one or more input channels with an ADC. These ways are known as conversion modes and I will cover the most popular conversion modes next.

### Single Channel/Single Conversion

This is the absolute simplest mode. [Figure 9-4](#ch9.xhtml_ch9fig4) shows a block diagram for this mode.

![images](fig09-04.jpg)

**Figure 9-4**   *Single channel/single conversion ADC mode block diagram.*

In this mode, the ADC takes or more accurately samples the analog voltage present on a selected input line or channel and converts that voltage to a digital number. The number is then read from the ADC and used in any application that requires it.

### Multi-channel Scan/Single Conversion

This mode is a little more complex than the previous one. In this mode, multiple input analog lines are sampled and the sampled voltage levels are then converted into digital numbers. The block diagram for this mode is shown in [Figure 9-5](#ch9.xhtml_ch9fig5).

![images](fig09-05.jpg)

**Figure 9-5**   *Multi-channel scan/single conversion ADC mode block diagram.*

One of the exceptionally nice features for this mode is that each channel is independent and may be configured to have different sample rates, trigger sources, and other custom items. This feature is implemented by using a ranks object. By using ranks, the MCU does not have to stop and reconfigure each channel for its custom configuration. This mode only does one scan and the result numbers are often directly stored in a memory using a direct memory access (DMA).

### Single Channel/Continuous Conversion

In this mode, a single channel is continuously being sampled and the resulting digital numbers are continuously being stored in memory. This mode almost always uses DMA to alleviate excessive load on the MCU. This mode is ordinarily use for real-time monitoring of sensors or other environmental devices.

### Multi-Channel Scan/Continuous Conversion

In this mode, multiple channels are being continuously sampled and the resulting digital numbers are stored in memory. This mode demands that DMA be used to alleviate an intolerable computation load on the MCU. This mode is ordinarily used for comprehensive real-time monitoring of sensors or other environmental devices.

## Channels, Groups, and Ranks

The number of channels that can be converted varies with the particular STM MCU being used. That number is set at 16 for the STM32F302R8 MCU used in the Nucleo project board. Sequences of channel conversions may be set up within independent collections known as groups. Channels may be arranged in any order within a specific group.

Input channels are hardware based and thus fixed and linked to specific MCU pins, that is, IN0 is the first channel, IN1 the second, and so on. They can, however, be logically reordered to form a custom sampling sequence within a group. The reordering of channels is done by assigning the input channel to an index ranging from 1 to 16. This index is called rank in the HAL.

[Figure 9-6](#ch9.xhtml_ch9fig6) shows this concept. Although the IN3 channel in the figure is fixed, for example, it is connected to PA3 pin in an STM32F302R8 MCU, it can be assigned to the rank 1 to make it the first channel to be sampled.

![images](fig09-06.jpg)

**Figure 9-6**   *ADC diagram showing channels and ranks.*

The following C struct is defined for an `ADC_ChannelConfTypeDef`. Each struct member will separately be discussed after the struct definition.

![Images](c0199-02.jpg)

The `ADC_ChannelConfTypeDef` struct members are defined in the following list:

`uint32_t Channel;`—This value specifies the channel to configure into ADC regular group. This parameter can be any value of the following ADC_CHANNEL defines:

![Images](c0199-05.jpg)

`uint32_t Rank;`—This value specifies the rank in the regular group sequencer. This parameter must be a number between Min_Data = 1 and Max_Data = 16: This parameter can be any value of the following ADC_REGULAR_RANK defines:

![Images](c0200-01.jpg)

`uint32_t SamplingTime;`—The sampling time value to be set for the selected channel in units of ADC clock cycles. The total conversion time is the addition of sampling time and processing time (12 ADC clock cycles at ADC resolution 12 bits, 11 cycles at 10 bits, 9 cycles at 8 bits, 7 cycles at 6 bits). This parameter can be any value of the following ADC_SAMPLETIME defines:

![Images](c0200-03.jpg)

***CAUTION:*** *This parameter updates the parameter property of the channel, which can be used into regular and/or injected groups. If this same channel has been previously configured in the other group (regular/injected), it will be updated to last setting. In case of usage of internal measurement channels (VrefInt/Vbat/TempSensor), sampling time constraints must be respected (sampling time can be adjusted in function of ADC clock frequency and sampling time setting).*

`uint32_t Offset;`—Reserved for future use, can be set to 0.

## ADC Demonstration

The ADC, like many STM peripherals, can be controlled using one of three methods:

•   Polling

•   Interrupt

•   DMA

This first demonstration will use polling as the control approach because it is the simplest and will allow the focus to be mainly on the ADC process.

The initial step is to create a reference to a `ADC_HandleTypeDef` struct and then assign the appropriate values to struct members that will define the ADC instance to be implemented. This new instance will next be configured using the `ADC_InitTypeDef` struct, which requires a reference to the now defined `ADC_HandleTypeDef` struct. It will time to initialize and start the ADC once all the `ADC_InitTypeDef` struct members have been defined. The initialize and start commands are accomplished using these calls:

![Images](c0201-06.jpg)

The ADC will then either do one conversion if the single mode was selected or continue with a stream of conversions if the continuous mode was selected. In the case of the single mode, the `HAL_ADC_Stop()` method must first be called to stop the ADC thread and then the `HAL_ADC_Start()` method must be called again to do another conversion.

Any application desiring access to the converted data must use the following method when using polling to determine when an ADC conversion has finished and the data is available:

![Images](c0201-09.jpg)

The argument methods are a pointer to the `ADC_HandleTypeDef` struct and an integer named Timeout representing the maximum number of milliseconds to wait for data to be available from the ADC register. It is also possible to use the define HAL_MAX_DELAY for the Timeout value, which will cause the system to wait indefinitely for data. I would not recommend that approach because it has the potential to “hang” the system without any apparent symptom.

You must use the following method to actually transfer the data from the ADC register to any user application:

![Images](c0201-11.jpg)

It is now appropriate to discuss the Analog Devices TMP36 temperature sensor, which I introduced at the chapter’s start. This sensor will be the analog voltage source used for the ADC demonstration.

### Analog Devices TMP36 Temperature Sensor

An image of this sensor has been shown in [Figure 9-1](#ch9.xhtml_ch9fig1). It is housed in a regular TO-92 plastic case with three leads as shown in the figure. It does, however, contain quite a bit of internal components that allow it to output a DC voltage that is proportional to the ambient temperature surrounding its case. This sensor is also very inexpensive and is readily available from a number of online sources. The sensor specifications are listed below:

•   Size: TO-92 package (about 0.2″ × 0.2″ × 0.2″) with three leads

•   Temperature range: –40°C to 150°C/–40°F to 302°F

•   Output range: 0.1V (–40°C) to 2.0 V (150°C) (decreasing accuracy after 125°C)

•   Power supply: 2.7 V to 5.5 V only, with a typical 0.05-mA current draw

[Figure 9-7](#ch9.xhtml_ch9fig7) shows to what each lead should be connected.

![images](fig09-07.jpg)

**Figure 9-7**   *TMP36 lead connections.*

The leads should be connected to the Arduino protoboard, as detailed in [Table 9-1](#ch9.xhtml_ch9tab1).

The temperature is very easy to calculate using the following equation:

°C = [(Vout in mV) – 500] /10

The equivalent temperature in °F is also easily calculated using this conversion equation:

°F = (9 * °C/5) + 32

It is now time to discuss the main.c file as all the precursor items have been introduced and explained.

### Enabling ADC1

I will now need to enable the ADC1 alternative function in order to have the analog-to-digital conversion function. You configure ADC1 when creating a new project and the Pinout window is displayed. [Figure 9-8](#ch9.xhtml_ch9fig8) shows how the ADC1 peripheral is enabled by selecting IN1 Single-ended from the ADC1 IN1 dropdown menu.

![images](fig09-08.jpg)

**Figure 9-8**   *Enabling the IN1 channel in ADC1.*

The CubeMX application will automatically insert an initialization method `static void MX_ADC1_Init(void)` in the main.c file when the ADC1 functionality is enabled.

The appropriate ADC parameters are automatically set for you based upon the parameters you set in the ADC1 IP tree view, as shown in the following code snippet:

![Images](c0204-02.jpg)

### Connecting ADC1 to the TMP36 Sensor

[Figure 9-9](#ch9.xhtml_ch9fig9) shows how I connected the TMP36 temperature sensor to the ADC1 internal peripheral using a solderless breadboard, jumper leads, and the Arduino protoboard.

![images](fig09-09.jpg)

**Figure 9-9**   *Interconnections between the TMP36 sensor and the Arduino protoboard.*

The TMP36 lead connections have been previously detailed in [Table 9-1](#ch9.xhtml_ch9tab1). You will need three jumper leads to connect the sensor to the Arduino protoboard.

![images](tab09-01.jpg)

**Table 9-1**   *TMP36 Lead Connections*

At this point, all the prerequisites have been introduced that are needed to demonstrate an actual ADC program.

## ADC Demonstration Software

The following program is based on the USART program shown in the previous chapter. This step was taken because the processed ADC output is required to be displayed in a terminal window. The main.c file now has a new method that configures and initializes the ADC1 internal peripheral.

There is also new functional code that runs within the forever loop. This code is shown in the following code snippet with detailed explanations following the listing:

![Images](c0206-01.jpg)

All the statements within the code snippet are discussed below:

•   `HAL_ADC_Start(&hadc1);`—Starts the ADC1 internal peripheral.

•   `HAL_ADC_PollForConversion(&hadc1, 100);`—Waits for an end-of-conversion (EOC) signal before proceeding to the next instruction. The 100 value is the maximum time in milliseconds to wait for the EOC signal. This is a blocking type instruction.

•   `raw = (double) HAL_ADC_GetValue(&hadc1);`—Transfer the value from the adc output register to the `raw` variable. This is a 12-bit value with a maximum numerical value of 4095, which is roughly equivalent to 5 V. The value is also cast to a double format.

•   `raw = raw * 0.452;`—Conversion from a raw count to an absolute mV output. The scaling factor 0.452 was determined using a precision voltage measurement.

•   `value = (raw - 500.0)/10;`—The raw mV value is converted to a °C temperature using the TMP36 equation.

•   `value = (9*value)/5 + 32;`—Classic equation to convert from °C to °F.

•   `sprintf(msg, “%f\r\n”, value);`—Causes the double variable `value` to be converted to a string with a carriage return and line feed concatenated to the value.

•   `HAL_UART_Transmit(&huart2, (uint8_t*) msg, 20, 100);`—Performs the actual transmission of the data from the MCU to the terminal program

•   `HAL_Delay(1000);`—Inserts a one second delay between samples.

The complete main.c program is listed below:

![Images](c0207-06.jpg)

![Images](c0208-01.jpg)

![Images](c0209-01.jpg)

![Images](c0210-01.jpg)

![Images](c0211-01.jpg)

### Test Run

The program was then built and downloaded into the project board. I then started the Realterm terminal program to display the communication stream from the board. [Figure 9-10](#ch9.xhtml_ch9fig10) shows the terminal output.

![images](fig09-10.jpg)

**Figure 9-10**   *Terminal output.*

I tried cooling and heating the sensor and saw the sensor reacting according to the ambient temperature.

### Summary

Analog-to digital conversion (ADC) was the chapter’s topic. There was an explanation of how the 16-channel, 12-bit ADC works within the MCU. It uses a successive approximation technique to acquire precise numerical samples of a continuously varying analog input.

The discussion next turned to how the HAL framework supports the ADC function. I went through the two C structs that both configure and initialize the ADC peripheral. The discussion also included the various conversion modes, channels, groups, and ranks.

A full-scale ADC demonstration closed out the chapter. A TMP36 temperature sensor was used as an analog voltage source to the ADC. The program used the USART2 peripheral to stream out continuous temperature readings to a terminal window.

## 10

## Pulse Width Modulation (PWM)

This chapter concerns pulse width modulation (PWM), which is a digital signal easily generated by a MCU for a variety of purposes. These purposes commonly include controlling the following:

•   A standard servo motor’s position

•   The rotational speed of a continuous rotation servo

•   The luminescence of a light emitter

•   The rotation speed of a standard electric motor with external driver circuitry

•   A photovoltaic solar battery charger

•   The maximum power-point track

•   An output waveform such as sine, triangle, or square

•   An acoustic sound generator

This chapter’s projects will demonstrate how to control the luminescence (light intensity) of a normal LED, the color and luminescence of a tricolor LED, and the positioning of a standard servo motor.

It is wise to first discuss the nature and properties of a PWM signal before proceeding to show how to generate that using the STM project board. [Figure 10-1](#ch10.xhtml_ch10fig1) is a typical PWM signal with various properties annotated in the figure.

![images](fig10-01.jpg)

**Figure 10-1**   *Typical PWM signal.*

The first thing to note is that the signal is repetitive with a frequency around 50 Hz or an equivalent 20 ms period. This frequency is very common in servo control and it will be what I will use for the chapter projects. However, there is nothing limiting about this frequency and you can use any value up to the limit of what the MCU can support.

The second important feature is the duty cycle, which is a percentage of the amount of time the signal is in a high state to the total period, which is the sum of the high and low times. Duty cycle is often considered the primary property for a PWM signal, for it solely determines the servo position and LED luminescence.

It turns out that each type of device being controlled by PWM acts differently with the signal. I will describe each specific interaction when I go through the device demonstration.

### General-Purpose Timer PWM Signal Generation

PWM signals are generated only by using either an advanced or a general purpose (GP) timer. This section describes the process on how this is done.

The signal generation is relatively simple and involves using a timer in an upcounting mode. The top portion of [Figure 10-2](#ch10.xhtml_ch10fig2) shows a timer counting up from 0 to a maximum 16-bit count equal to 65535.

![images](fig10-02.jpg)

**Figure 10-2**   *PWM signal generation.*

Each GP timer has a series of registers known as compare capture registers (CCRx), which store a number. When the upcounting reaches that number, an event is generated that depends on the timer mode. If the timer is set for a direct output as is the case for this PWM mode, then the event will be to turn on the channel associated with the CCRx register. In [Figure 10-2](#ch10.xhtml_ch10fig2), channel 1 is switched high when the count reaches 52428\. The channel remains high until the timer counter reaches the maximum count (MAX) and overflows or resets as shown in the top waveform. The net result of this action is that a repetitive pulse is emitted from the channel 1 line with a 20% duty cycle. The following equation relates the timer count with the duty cycle (DC):

![Images](c0215-01.jpg)

This equation may be rearranged to find the CCRx value given a desired duty cycle:

![Images](c0215-02.jpg)

In [Figure 10-2](#ch10.xhtml_ch10fig2), I have also shown an additional channel output with a desired 60% duty cycle but no specific count shown for the CCRx register. I will use the second form of the equation to solve for T[2], which is the count value to be stored in register CCR2:

![Images](c0215-03.jpg)

Therefore, storing a value of 26214 in CCR2 will cause a 60% duty cycle pulse train to be generated from TIM2’s channel 2 output. Please note that the numbers I used for this calculation are relative in the sense that the actual CCRx numbers stored depend upon the real timer clock rate. You will shortly see that the numbers are much smaller, but the principle to figure them out is the same.

The TIM2 GP timer I used for PWM generation has a maximum of four output channels, meaning that it is possible to simultaneously generate four synchronized PWM signals using a single GP timer. One of the following demonstrations uses three channels, which is ample to demonstrate this capability.

### Timer Hardware Architecture

[Figure 10-3](#ch10.xhtml_ch10fig3) is a portion of the GP timer block diagram highlighting the multi-channel outputs and associated CCRx registers.

![images](fig10-03.jpg)

**Figure 10-3**   *GP timer block diagram with four output channels.*

The architecture is very straightforward, showing that each CCRx register has an input from the common timer counter (CNT) register as well as its own prescaled clock-rate input. This arrangement enables a very flexible PWM pulse train output to be implemented.

It is now time to describe how the HAL software enables PWM signal generation.

### PWM Signals with HAL

The HAL framework uses a C struct named `TIM_MasterConfigTypeDef` to configure the timer peripheral generating a PWM signal. Each member will separately be discussed after the struct definition.

![Images](c0216-02.jpg)

The `TIM_MasterConfigTypeDef` struct members are briefly defined in the following list:

`uint32_t MasterOutputTrigger;`—This value specifies the behavior of the trigger output (TRGO). This parameter can be any value of the following defines:

`uint32_t MasterSlaveMode;`—This is used to enable/disable the master/slave mode of a timer. This parameter can be one of the two values of the following defines:

![Images](c0216-06.jpg)

A PWM timer configured using the `TIM_MasterConfigTypeDef` struct must further be initialized using the `TIM_OC_InitTypeDef` C struct, which is defined as follows:

![Images](c0218-02.jpg)

The `TIM_OC_InitTypeDef` struct members are briefly defined in the following list:

`uint32_t OCMode;`—Specifies the output compare mode. This parameter can be any value of the following defines:

`TIM_OCMODE_TIMING`—The comparison between the output compare register (CCRx) and the timer counter (CNT) has no effect on the output, which is known as a frozen mode.

`TIM_OCMODE_ACTIVE`—Set the channel output to active level on CCRx match.

`TIM_OCMODE_INACTIVE`—Set channel output to inactive level on CCRx match.

`TIM_OCMODE_TOGGLE`—Toggle channel output when the timer counter (CNT) matches the CCRx.

![Images](c0218-03.jpg)

`TIM_OCMODE_FORCED_ACTIVE`—Force channel output high independently from the timer counter (CNT) value.

`TIM_OCMODE_FORCED_INACTIVE`—Force channel output low independently from the timer counter (CNT) value.

***NOTE***  *PWM Mode 1: When the timer is upcounting, the channel will be active for as long as the Period is less than the Pulse, otherwise it is inactive. In a downcounting mode, the channel is inactive for as long as the Period is greater than the Pulse, otherwise it is active.*

*PWM Mode 2: When the timer is upcounting, the channel will be inactive as long as the Period is less than the Pulse, otherwise it is active. In downcounting mode, the channel is active for as long as the Period is greater than the Pulse, otherwise it is inactive.*

`uint32_t Pulse;`—This value be stored inside the CCRx register and it establishes when the output is triggered.

`uint32_t OCPolarity;`—Define the output channel polarity when the CCRx registers matches with the CNT. This parameter can be one of the two values of the following defines:

![Images](c0219-03.jpg)

`uint32_t OCNPolarity;`—Define the complementary output polarity. It is a mode available only in TIM1 and TIM8 advanced timers, which allow two additional dedicated channels to generate complementary signals, i.e., when the channel 1 is HIGH then channel 1N is LOW and vice versa. This feature is especially useful for motor control applications. This parameter can be one of the two values of the following defines:

![Images](c0219-05.jpg)

`uint32_t` `OCFastMode;`—Specifies the fast mode state. This parameter is valid only in PWM1 and PWM2 mode. This parameter can be one of the two values of the following defines:

![Images](c0219-07.jpg)

`uint32_t OCIdleState;`—Specifies the state of the channel output compare pin during the timer idle state. This parameter can be one of the two values of the following defines:

![Images](c0219-09.jpg)

***NOTE***  This parameter is available only in TIM1 and TIM8 advanced timers.

`uint32_t OCNIdleState;`—Specifies the state of the complimentary channel output compare pin during the timer idle state. This parameter can be one of the two values of the following defines:

![Images](c0220-02.jpg)

***NOTE***  *This parameter is available only in TIM1 and TIM8 advanced timers.*

## Enabling the PWM Function

You now need to enable the PWM alternative function in order to have the pulse width modulation function. The timer TIM2 is initially configured when creating the new project and having the Pinout window displayed. [Figure 10-4](#ch10.xhtml_ch10fig4) shows how TIM2 peripheral with PWM functionality is enabled in the Pinout view by selecting PWM direct output for channel 1 in TIM2\. The PA1 pin is the channel 1 output.

![images](fig10-04.jpg)

**Figure 10-4**   *Enabling timer TIM2 with PWM output on channel 1.*

The CubeMX application will automatically insert an initialization method `static void MX_TIM2_Init(void)` in the main.c file when the TIM2 PWM function is enabled. Some additional parameters should also be set in the TIM2 object using the CubeMX Configuration tab, as shown in [Figure 10-5](#ch10.xhtml_ch10fig5).

![images](fig10-05.jpg)

**Figure 10-5**   *Configuration menu settings.*

All of the initial PWM parameters are automatically set for you in the C code based upon the parameters you set in the TIM2 PWM IP tree view and the Configuration menu as shown in the following code snippet:

![Images](c0221-01.jpg)

![Images](c0222-01.jpg)

### PWM Demonstration Software

The newly generated main.c file now has a method that configures and initializes the TIM2 internal peripheral with a PWM output on its channel 1\. There is no functional code running within the forever loop. The PWM signal generation is all done automatically in the background. This code is shown in the following code listing:

![Images](c0222-02.jpg)

![Images](c0223-01.jpg)

![Images](c0224-01.jpg)

![Images](c0225-01.jpg)

![Images](c0226-01.jpg)

![Images](c0227-01.jpg)

You should note that I set the prescaler to a 655 value. This meant that the TIM2 clock input would be at a frequency approximately equal to 977 kHz with a period of 10.23 µs. This value ensured that the timer resolution would allow for setting very precise pulse widths.

## Demonstration One

This demonstration uses the values set during the initial configuration to generate a 50% duty cycle waveform. The program was first built and then downloaded into the project board. I used a USB oscilloscope to observe the PWM signal generated from the TIM2, channel 1 output, which is emitted from pin PA1. [Figure 10-6](#ch10.xhtml_ch10fig6) shows this waveform.

![images](fig10-06.jpg)

**Figure 10-6**   *Fifty percent duty-cycle PWM waveform.*

You should be able to see that the period of the over signal is 20 ms and the high time for the pulse is 10 ms, which creates the 50% duty cycle as expected. This waveform used a prescaler value equal to 655, which caused each timer count to be 10.23 µs as discussed above. The Period value was set at 1960, which means the actual period time is 1960 times 10.23 µs or 20050.8 µs, equivalent to 20.0508 ms. That was close enough for my purposes. The CCR1 register held a value of 980, which meant the output switched at 980 times 10.23 µs or 10025.4 µs, equivalent to 10.0254 ms. This is extremely close to a 50% duty cycle for all practical purposes. This demonstration proved that the PWM generation was working as desired.

[Table 10-1](#ch10.xhtml_ch10tab1) is provided as a handy reference showing a series of CCRx values that will generate a respective duty cycle given that value. Note that the small duty cycles shown at the table’s beginning are important for the servo control demonstration. This table is based upon a 50 Hz or 20 ms period PWM signal.

![images](tab10-01.jpg)

**Table 10-1**   *CCRx Values and Corresponding Duty Cycles and Pulse High Times*

## Demonstration Two

This demonstration controls the intensity or luminescence of a single, red LED, using a PWM output as shown in the previous demonstration. The only parameter to be varied is the CCRx value assigned in the main method by this statement:

![Images](c0228-01.jpg)

I chose to vary this value by editing the main.c file and then quickly rebuilding it. This process was very fast and not cumbersome at all. You could also set up an OpenOCD session and adjust the value in a dynamic fashion, but I found the edit, build, and download process to be very convenient without the bother of creating a telnet session. I would suggest you try both approaches and use whichever you find useful and productive.

### Connecting Channel 1 PWM Output to an LED/Resistor

[Figure 10-7](#ch10.xhtml_ch10fig7) shows the connections for the same LED/resistor combination, which I earlier used for the project demonstration in [Chapter 5](#ch5.xhtml_ch5). The LED/resistor is connected between PA1 and ground using the Arduino protoboard.

![images](fig10-07.jpg)

**Figure 10-7**   *LED/resistor connected on the Arduino protoboard.*

### Test Results

I observed that the LED luminescence did vary considerably with the duty cycle of the applied PWM signal. You should realize one important distinction between dimming an incandescent bulb and an LED. The incandescent bulb intensity corresponds to the average voltage applied to it, while the LED luminescence depends on your eye’s integrative response. By this, I mean the voltage applied to the LED is at a constant level, but the time interval applied varies with the duty cycle. The human eye will tend to integrate or average out the LED light intensity and thus perceive different intensities for varying duty cycles. The eye also has a nonlinear relationship between actual luminance and perceived brightness, as shown in [Figure 10-8](#ch10.xhtml_ch10fig8).

![images](fig10-08.jpg)

**Figure 10-8**   *Human eye brightness perception.*

What this all means is that the eye will more easily recognize different LED luminescence at small duty cycles but will not perceive any significant differences as the duty cycle increases. There are equations that model the eye brightness to luminance relationship quite well and have been codified as the CIE1931 lightness formula. White light LED manufacturers have modified their products using this relationship to make their commercial LEDs have a linear dimming property. I have not done this with this single LED demonstration, but it is quite doable and you would put the code into the main.c forever loop.

I did try to capture the intensity difference between 100% and 10% duty cycles. [Figure 10-9](#ch10.xhtml_ch10fig9) is a composite photograph with the 100% PWM on the left and the 10% PWM on the right.

![images](fig10-09.jpg)

**Figure 10-9**   *100% and 10% PWM signal-duty cycles applied to a red LED.*

The camera shutter speed that was required for these images was fairly long, which tended to make the 10% image much brighter than it actually was. I guess you will just have to duplicate this demonstration and see the actual duty cycle versus perceived luminance for yourself.

## Demonstration Three

In this demonstration I will be controlling a RGB LED that has three input lines, one for each color. GP timer TIM2 will be reconfigured to have three PWM outputs connected to each of the LED’s lines. The PWM lines will control both the LED color and luminescence based on the duty cycle set on each line.

The first step is to create a new CubeMX project to handle the additional PWM lines. [Figure 10-10](#ch10.xhtml_ch10fig10) shows the Pinout view where I have configured TIM2 for four channel outputs, of which I will use the first three to control the RGB LED.

![images](fig10-10.jpg)

**Figure 10-10**   *Enabling timer TIM2 with PWM output on channels 1 to 4.*

The configuration menu is exactly the same as previously shown in [Figure 10-5](#ch10.xhtml_ch10fig5).

### Connecting Channel PWM Outputs to a RGB LED

[Figure 10-11](#ch10.xhtml_ch10fig11) is a schematic showing the connections between the RGB LED and the timer GPIO pins as connected on the Arduino protoboard. Note that each LED line has a series current limiting resistor to protect both the GPIO pin and the RGB LED.

![images](fig10-11.jpg)

**Figure 10-11**   *RGB to Arduino protoboard connection schematic.*

The timer TIM2 channel outputs are on the following pins:

•   Channel 1—PA0

•   Channel 2—PA1

•   Channel 3—PB10

•   Channel 4—PB11

[Figure 10-12](#ch10.xhtml_ch10fig12) shows the physical setup for a RGB LED connected to an Arduino protoboard.

![images](fig10-12.jpg)

**Figure 10-12**   *Physical RGB LED connections to an Arduino protoboard.*

### Software Modifications

A modified `MX_TIM2_Init` method will be added to the main.c file based on the additional channel outputs. This new method is listed below:

![Images](c0234-02.jpg)

![Images](c0235-01.jpg)

There is also some new code that must be entered into the main method. This new code is listed below:

![Images](c0235-02.jpg)

Note that each of the RGB channels was initialized at a 50% duty cycle.

### Test Results

The RGB LED initially showed a bright white light, which was expected because all the individual LED components had the same duty cycle. I then reset the individual CCRx registers to separately test each color and confirmed that they were operating properly. I also tried varying the duty cycles to create different colors with little success because of the way the RGB LED was constructed. It did not merge the light from each colored LED and therefore did not properly create an alternate color, which you can do if you were mixing paint. I believe I would have been successful if I had used a more expensive RGB LED with some built-in optics, but unfortunately all I had was a very inexpensive RGB LED. In any case, the objective for this demonstration was to show you how to create and use multiple PWM outputs, which I believe was achieved.

## Demonstration Four

This last demonstration will focus on using a single PWM signal to control a hobby-grade servo motor. I will be using the same program that was used for the first two demonstrations and no code modifications are required. I will start the demonstration by reviewing some basic facts regarding how analog servos are controlled.

### Analog Servo Control

An analog servo is essentially an electric motor that has a built-in electronic circuit that converts specific pulse widths into a proportional rotation. The specifications for hobby-grade analog servos are fairly “relaxed” meaning that there are loose tolerances relating pulse width to physical rotation. This is mainly due to the use of very low cost components in both the electrical and mechanical components that comprise the servo. [Table 10-2](#ch10.xhtml_ch10tab2) details pulse width and expected rotation.

![images](tab10-02.jpg)

**Table 10-2**   *Pulse Width and Servo Rotation*

An analog servo should not move from its neutral position when it is sent a repetitive 1.5-ms pulse signal. A 1.0-ms pulse train will cause it to rotate its main shaft counter-clockwise 60°if viewed from head-on. Similarly, a 2.0-ms pulse train will cause it to rotate clockwise 60°. However, loose tolerances come into play and often the degree of rotation can be 10° to 15°, more or less.

In all cases, the pulse train frequency is set at a nominal 50 Hz or 20 ms period.

[Figure 10-13](#ch10.xhtml_ch10fig13) shows the hobby-grade servo I used for this demonstration. It is a Hitec model HS-311, which is a reliable, well-built servo.

![images](fig10-13.jpg)

**Figure 10-13**   *Hitec model HS-311 analog servo.*

This servo takes quite a bit of current to operate, somewhat in excess of what the STM project board can provide. Consequently, I used a separate supply for it as may be seen in the [Figure 10-14](#ch10.xhtml_ch10fig14) connection schematic.

![images](fig10-14.jpg)

**Figure 10-14**   *Servo connection schematic.*

The servo control signal from the PWM output only requires several milliamperes, which is well within the GPIO pin drive capabilities.

[Figure 10-15](#ch10.xhtml_ch10fig15) shows the waveform for the 1.5-ms neutral position signal. It is a nice, clean signal with sharp rise and fall times, which are important for proper servo control.

![images](fig10-15.jpg)

**Figure 10-15**   *1.5-ms servo control signal.*

The 1.0-ms and 2.0-ms waveforms are very similar except for the pulse width.

[Figure 10-16](#ch10.xhtml_ch10fig16) shows the physical setup with the analog servo connected to a solderless breadboard, which in turn is connected to the Arduino protoboard with jumper wires.

![images](fig10-16.jpg)

**Figure 10-16**   *Servo test setup.*

### Test Results

I first changed the CCR1 value to 148, which causes a 1.5-ms pulse width to be generated. The servo immediately moved to its neutral position after the program was downloaded into the project board. I repeated the previous step with a CCR1 equal to 98, which generates a 1.0-ms pulse width. The servo responded by moving its main shaft 60° counter-clockwise. Finally, I changed CCR1 to 196, which generates a 2.0-ms pulse width. The servo’s main shaft rotated clockwise 120° as expected.

The servo performed flawlessly and showed no signs of jitter or vibration, which sometimes occurs with using hobby-grade servos.

I next added some functional code and placed it in the forever loop to continuously exercise the servo, thus eliminating the need to edit, rebuild, and download the controlling program.

## Adding Functional Test Code

The following C code was placed within the main.c file in order to continuously control the servo. This code caused the servo main shaft to slowly oscillate between the ±60° end points.

![Images](c0239-01.jpg)

## Test Results

I observed the servo main shaft to slowly oscillate between the end points as expected after the modified code was downloaded into the project board.

This final demonstration concludes the chapter. I believe I have provided you with a sufficient background that will enable you to successfully use servos with a STM Nucleo board.

### Summary

I started this chapter on pulse width modulation (PWM) by explaining what makes up a PWM signal and detailing certain key properties of that signal. This was followed by a brief discussion of how the STM timer hardware generates a PWM signal.

Next came a discussion on how the HAL framework is used to both configure and initialize a general purpose (GP) timer to emit a PWM signal.

A complete C code listing was shown that generated a PWM signal with a 50% duty cycle and a 50-Hz output frequency.

Next followed the first of four PWM demonstrations. The first PWM demonstration just output the 50% duty cycle waveform that was generated by the project board after the code was built and downloaded into the board.

The second demonstration used a varying duty-cycle waveform to dim and brighten a red LED.

The third demonstration used multi-channel PWM waveforms to control both the color and intensity of a RGB LED.

The fourth and final demonstration illustrated how to control a standard analog servo using PWM signals.

## 11

## Direct Memory Access (DMA) and the Digital-to-Analog Converter (DAC)

This chapter content is carefully chosen to explain direct memory access (DMA) and the very useful digital-to-analog converter (DAC) peripheral, which takes advantage of efficient DMA data transfers. There are also several demonstration projects shown in the chapter, which show both DMA and DAC operations. The last one shows how to use DMA with the DAC peripheral

### DMA

Data is normally transferred by using instructions executed by the Cortex-M core processor. This data is normally sent to or from internal memories and peripherals. This data transfer process consumes valuable processor cycles that could otherwise be put to use within a constrained embedded system. This is the reason why the DMA controller was designed. It can assume the data transfer process in many cases and allow the core processor to take on other critical embedded system processes.

Technically, the DMA controller can be considered a peripheral device; however, I prefer to think of it as more like a co-processor than a peripheral. Unlike any other peripheral, the DMA controller can take on the role of being a bus master, which is not allowed for any other device other than the core processor itself. In fact, thinking of the DMA controller as more of a bus controller is a good way to view this device.

[Figure 11-1](#ch11.xhtml_ch11fig1) is a block diagram for the DMA controller used in the project board’s STM32F302R8 MCU. This figure will be very useful in explaining how the DMA controller works.

![images](fig11-01.jpg)

**Figure 11-1**   *DMA block diagram.*

***NOTE***  DMA2, SPI1, TIM3, TIM4, UART4, UART5, and ADC2 are not available in the STM32F302R8 MCU.

It would be worthwhile to consider some of the basics of data transfers before going into the specifics of DMA operations.

## Basic Data Transfer Concepts

[Figure 11-2](#ch11.xhtml_ch11fig2) is a simplified system block diagram where all the DMA components have been removed from [Figure 11-1](#ch11.xhtml_ch11fig1). The purpose of this diagram is to focus on how data transfers happen between the core processor and all remaining system peripherals.

![images](fig11-02.jpg)

**Figure 11-2**   *Data transfers between the core processor and system peripherals.*

You should clearly see that all data transfers between the core Cortex-M processor and any peripheral or internal memory must go through either the Bus Matrix or FLITF blocks. There is simply no other way that data can reach the processor. Every data transfer requires some amount of processor cycles to complete. For example, the processor must handle all data sent by an external device connected to a UART peripheral where that data is to be designated to be stored in SRAM. It is important to realize that the processor does not modify or change the data in any way, but simply sends it along to the proper memory storage locations. This requirement for core processor involvement ties up precious cycles that otherwise could be utilized for more efficient operations. A somewhat analogous model is where data is represented by cars and the processor by a city. Cross-country drivers wanting to go to a distant location are forced to go through a city with all its traffic lights and congested streets. It would be much better for the drivers if a bypass highway were available, allowing them to avoid going through the city. The DMA controller plays the role of the bypass.

Returning to [Figure 11-1](#ch11.xhtml_ch11fig1), you should be able to see that DMA1 controller, in the case of the STM32F302R8 MCU, connects directly to the Bus Matrix. This controller, as I earlier mentioned, is set up to be a bus controller or master and thus is able to configure the Bus Matrix to directly connect data between peripherals and internal memory, memory to memory, or even to another peripheral. These configurations are naturally named as follows:

•   Peripheral-to-memory transfers

•   Memory-to-peripheral transfers

•   Peripheral-to-peripheral transfers

•   Memory-to-memory transfers

The Bus Matrix controls the access of both the core processor and the DMA controller to various data busses, memory, and peripherals. It implements this control with a Round Robin algorithm, which ensures equitable access to both controllers. [Figure 11-3](#ch11.xhtml_ch11fig3) is a block diagram illustrating how the Bus Matrix is connected with all the system components.

![images](fig11-03.jpg)

**Figure 11-3**   *Bus Matrix block diagram.*

The Bus Matrix is a complex circuit that interconnects the following master and slave devices:

•   Core Cortex-M processor (master)

•   DMA controller(s) (master)

•   Flash memory interface (FLITF) using the ICODE (slave)

•   Flash memory interface (FLITF) using the DCODE buss (slave)

•   Direct connection to SRAM (slave)

•   Advanced High-Speed Bus 1 (AHB1), which connects to the Advanced Peripheral Busses (AHB1 and AHP2) through bridge circuits (Bridge 1 and Bridge 2) (slave)

•   Advanced Peripheral Bus (APB) connected to the GPIO pins (slave)

•   Direct connection to the ADC1 peripheral (slave)

## DMA Controller Details

Every STM32 DMA controller contains two master ports, one named the memory port, which connects to internal memory such as SRAM and flash. The other is named the peripheral port and it connects to the Advanced High-Performance Bus (AHB). The AHB in turn connects with the slave peripherals. In the STM32F302R8 DMA controller, the peripheral port can also connect to a memory control circuit permitting memory-to-memory transfers.

STM32 DMA controllers also have one slave port connected to the AHB bus. This allows the DMA controller to be programmed from the other master, that is, the core processor.

The STM32F302R8 DMA controller has seven independent and programmable channels, which are each connected to separate hardware lines. These are how the slave peripherals can request a response from the DMA controller. The exact nature and type of request is configured during the MCU hardware design phase. Different STM MCUs will have a varying numbers of channels as well as different request types depending upon the MCU design requirements.

There is also a priority assignment hardware unit, which allows different priorities to be assigned to the seven DMA request channels. Higher priorities will normally be assigned to fast peripherals needing immediate DMA response as well as to any memory accesses.

[Figure 11-4](#ch11.xhtml_ch11fig4) shows all seven DMA channels along with their respective peripheral request signals that are bound to them during the MCU design phase.

![images](fig11-04.jpg)

**Figure 11-4**   *DMA channel block diagram.*

[Figure 11-4](#ch11.xhtml_ch11fig4) is an important figure because it will be your ready reference to use when trying to determine which DMA channel to use for a given peripheral DMA request. It is very important to note that only one peripheral can be active on a given peripheral request line.

Notice in [Figure 11-4](#ch11.xhtml_ch11fig4) that the DMA channels have default priorities, which are fixed in hardware with channel 1 being the highest and progressing to channel 7 as the lowest. However, these default priorities may be overridden with user-assigned priorities, designed to determine which peripherals have preference when accessing the AHB. DMA channel lines are normally trigged through hardware signals from selected peripherals but they can also be activated by software. Software triggering is the means by which memory-to-memory transfers are activated.

## Using HAL with DMA

The HAL framework uses a C struct named `DMA_HandleTypeDef` to configure the DMA controller. Each member will separately be discussed after the struct definition.

![Images](c0246-02.jpg)

The `DMA_HandleTypeDef` struct members are briefly defined in the following list:

•   `DMA_Channel_TypeDef *Instance;`—This is the pointer to the DMA/Channel pair descriptor which will be used. For example, DMA1_Channel5 indicates the fifth channel of DMA1\. Recall that these designations are bound to peripherals during the MCU design. Refer to [Figure 11-4](#ch11.xhtml_ch11fig4) to see the channel-to-peripheral designations.

•   `DMA_InitTypeDef Init`;—This is an instance of the C struct `DMA_InitTypeDef`, which is used to configure the DMA/Channel pair. This value will be further explained below.

•   `HAL_LockTypeDef Lock;`—DMA locking object.

•   `__IO HAL_DMA_StateTypeDef State;`—DMA transfer state.

•   `void *Parent;`—This is a pointer used to keep track of the peripheral handlers associated with the current DMA/Channel. For example, if we are using a UART in DMA mode, this field will point to an instance of `UART_HandleTypeDef`.

•   `void (* XferCpltCallback)(struct __DMA_HandleTypeDef *hdma);`—This is a pointer to a callback function, which is used to signal user code that a DMA transfer is completed. It is automatically called by the HAL when a DMA interrupt is paired, by the function `HAL_DMA_IRQHandler()`.

•   `void (* XferHalfCpltCallback)(struct __DMA_HandleTypeDef *hdma);`—This is a pointer to a callback function, which is used to signal user code that a DMA transfer is completed, half-completed, or an error occurred. It is automatically called by the HAL when a DMA interrupt is paired by the function `HAL_DMA_IRQHandler()`.

•   `void (* XferErrorCallback)(struct __DMA_HandleTypeDef *hdma);`—This is a pointer to a callback function, which is used to signal user code that a DMA transfer has an error. It is automatically called by the HAL when a DMA interrupt is paired by the function `HAL_DMA_IRQHandler()`.

•   `__IO uint32_t ErrorCode;`—DMA error code.

The HAL framework uses a C struct named `DMA_InitTypeDef` to initialize the DMA controller. Each member will separately be discussed after the struct definition.

![Images](c0248-21.jpg)

![Images](c0249-01.jpg)

The `DMA_InitTypeDef` struct members are briefly defined in the following list:

•   `uint32_t Direction;`—This value defines the DMA transfer direction. This parameter can be any value of the following defines:

•   `DMA_PERIPH_TO_MEMORY`

•   `DMA_MEMORY_TO_PERIPH`

•   `DMA_MEMORY_TO_MEMORY`

•   `uint32_t PeriphInc;`—This value can automatically increment the peripheral register holding the data address to be transferred. This parameter can be one of the two values of the following defines:

•   `DMA_PINC_ENABLE`

•   `DMA_PINC_DISABLE`

•   `uint32_t MemInc;`—This value can automatically increment the memory port register holding the memory data address to be transferred. This parameter can be one of the two values of the following defines:

•   `DMA_MINC_ENABLE`

•   `DMA_MINC_DISABLE`

•   `uint32_t PeriphDataAlignment;`—This value set the sizes of the peripheral data elements to be transferred. This parameter can be any value of the following defines:

•   `DMA_PDATAALIGN_BYTE`

•   `DMA_PDATAALIGN_HALFWORD`

•   `DMA_PDATAALIGN_WORD`

•   `uint32_t MemDataAlignment;`—This value set the sizes of the memory data elements to be transferred. This parameter can be any value of the following defines:

•   `DMA_MDATAALIGN_BYTE`

•   `DMA_MDATAALIGN_HALFWORD`

•   `DMA_MDATAALIGN_WORD`

•   `uint32_t Mode;`—This value sets the DMA mode. In the normal mode, the DMA controller sends the specified amount of data from the source port to the destination port and then stops. The controller must be rearmed for another transfer. In the circular mode, the DMA controller sends the content of the source data buffer, resets to the first byte in source data buffer, and starts sending the buffer again. In the transmission interim, the peripheral will have had a chance to refill the source buffer so there will be fresh data in the source buffer. In this case, the source buffer is also called a ring buffer. The DMA circular mode is also called the continuous mode for obvious reasons. This parameter can be one of the two values of the following defines:

•   `DMA_NORMAL`

•   `DMA_CIRCULAR`

•   `uint32_t Priority;`—Use this value to assign a priority to a DMA channel. This parameter can be any value of the following defines:

•   `DMA_PRIORITY_LOW`

•   `DMA_PRIORITY_MEDIUM`

•   `DMA_PRIORITY_HIGH`

•   `DMA_PRIORITY_VERY_HIGH`

### Final Steps in Setting Up a DMA Transfer

There are just a few more steps required in order to configure a DMA transfer over a selected channel. These are as follows:

1.   Set up appropriate memory and/or peripheral port addresses

2.   Establish the size of the data transfer

3.   Arm the DMA controller

4.   Enable the DMA mode on the selected peripheral

The HAL framework abstracts the first three steps with the following statement:

![Images](c0250-05.jpg)

The fourth step is dependent on the selected peripheral. You will normally consult the STM data sheet, which describes the selected peripheral in order to determine how to enable the DMA transfer and to find out the exact channel it has been preassigned. Remember from the earlier discussion that peripherals have been preassigned channel numbers during the MCU design phase. In the following example, I will be demonstrating how to use USART2 peripheral in the DMA mode.

## Demonstration One

This first demonstration will involve sending a string using the USART2 peripheral operating in the normal DMA mode. There are just a few steps necessary to configure this demonstration:

1.   First configure the USART2 peripheral using the Pinout view in the CubeMX application as has been done several times in previous demonstrations.

2.   Set the DMA1 channel as follows (STM32F302R8 MCU) for the USART2 peripheral for a memory-to-peripheral transfer:

a.   USART2_TX = DMA1/CH7

b.   USART2_RX = DMA1/CH6

The following statement sets the USART2 peripheral DMA1, channel 7 to output characters to a terminal program:

![Images](c0251-01.jpg)

It must be put in the `main` method. In addition, there is no need to instantiate DMA1, channel 6 because no characters will be received from the terminal program in this demonstration.

3.   Enable the USART2 peripheral for DMA operations and arm the appropriate channel to execute the transfer.

The following statement enables the USART2 peripheral for DMA operations:

![Images](c0251-02.jpg)

It must be put in the `main` method.

### Program Listing

The following is the code listing for this demonstration. I have also provided some additional discussion regarding pertinent code segments following the listing.

![Images](c0252-01.jpg)

![Images](c0253-01.jpg)

![Images](c0254-01.jpg)

![Images](c0255-01.jpg)

![Images](c0256-01.jpg)

![Images](c0257-01.jpg)

I have first configured and initialized all the appropriate DMA setting in the main method. Some `DMA_InitTypeDef` struct members were not set because they are not needed in this demonstration and their values are not read during this particular DMA operation. The first three steps in the DMA preoperation sequence are as follows:

1.   Set up appropriate memory and/or peripheral port addresses.

2.   Establish the size of the data transfer.

3.   Arm the DMA controller.

These steps were all accomplished using the following statement:

![Images](c0257-03.jpg)

The fourth and the final step is to start the DMA operation for the selected peripheral. This was accomplished by the following statement:

![Images](c0257-04.jpg)

The seventh bit in the USART2 control register CR3 is named DMAT and is set to commence normal DMA operations for this peripheral.

The core processor has also been set up to poll to determine when the DMA operation has been completed. This operation was accomplished by the following statement:

![Images](c0257-05.jpg)

Polling for completion is completely appropriate for this demonstration simply because it is a “one-shot” occurrence and does not impede, nor conflict with any other MCU operations.

Finally, the USART2 peripheral is disarmed from further DMA operations by using the following statement:

![Images](c0258-01.jpg)

### Test Results

I observed that the user LED did light after the hex file was downloaded into the project board. However, I desired a better indication that the DMA operation did run successfully. To do this, I started the Realterm application and monitored the virtual communications port that is logically connected to the USART2 peripheral. [Figure 11-5](#ch11.xhtml_ch11fig5) shows the screen capture displaying the data message sent out from the peripheral.

![images](fig11-05.jpg)

**Figure 11-5**   *Realterm screen display.*

This absolutely confirmed that the USART2 peripheral transmitted the data message to memory via DMA.

This demonstration should now have convinced you of the DMA usefulness. It is time to introduce the DAC peripheral and really demonstrate how DMA can significantly improve MCU operations.

### DAC Peripheral

I will first explain the principles behind the DAC peripherals in order for you to understand how it requires rapid data transfers to operate efficiently.

## DAC Principles

The DAC design used in STM MCUs is based on a R-2R resistor ladder network concept. This concept is easily explained by referring to [Figure 11-6](#ch11.xhtml_ch11fig6).

![images](fig11-06.jpg)

**Figure 11-6**   *R-2R design concept.*

The resistive network acts like a programmable voltage divider between a reference voltage and ground. The usual reference voltage (V[ref]) for the STM DAC is the main 3.3-V supply. There is a 3-bit DAC, shown [Figure 11-6](#ch11.xhtml_ch11fig6), which makes it easy to discuss. In reality the DAC used in the project board has a 12-bit input.

The binary inputs shown in [Figure 11-6](#ch11.xhtml_ch11fig6) are switched between 0 V and V[ref] or 3.3 V. If a bit is high, it will cause its voltage input to weighted in the summed voltage output according to its bit position.

The output voltage (V[out]) for the 3 bit (*N* = 3) example for a given digit binary input (Value) is determined by the following equation:

![Images](c0259-01.jpg)

Therefore, if the maximum value equals 7 or in binary terms 111, the maximum V[out] will be:

![Images](c0260-01.jpg)

This result happens because the step size is 3.3/8 or 0.4125\. This is a rather large error and only happens in this case due to the small number of bits involved. For the real 12-bit STM DAC, the step size would only be 3.3/4096 or 0.00080566 V or roughly 0.8 mV. That step size will provide an excellent analog voltage representation for a digital number. Returning to the digital example, I have calculated all eight analog voltage outputs for all the possible binary combinations. These are shown in [Table 11-1](#ch11.xhtml_ch11tab1).

![images](tab11-01.jpg)

**Table 11-1**   *Binary Input vs Analog Voltage Output—3-bit DAC Example*

[Figure 11-7](#ch11.xhtml_ch11fig7) shows the analog voltage output in more start terms where it becomes very apparent that there is no smooth transition between binary input values due to the limited number of bits.

![images](fig11-07.jpg)

**Figure 11-7**   *Bar chart showing analog voltage outputs.*

[Table 11-1](#ch11.xhtml_ch11tab1) and [Figure 11-7](#ch11.xhtml_ch11fig7) provide more than ample proof that a sufficient number of bits must be present to have a somewhat smooth and continuous voltage output from a DAC. However, there will still be a small noise present even with a high number of bits present due to the inherent switching that is constantly happening with the DAC. This noise may be easily filtered out using an active low-pass analog filter. However, I will demonstrate that the DAC output is very clean and can be directly used as is without additional filtering.

A STM DAC also has the option of switching in a buffer output amplifier. This device will lower the DAC’s output impedance and provide additional drive current without the need to add an external output operational amplifier for this purpose.

It is now time to discuss the HAL software that can configure and initialize the STM DAC peripheral.

## HAL Software for the DAC

The HAL framework uses a C struct named `DAC_HandleTypeDef` to configure the DAC peripheral. Each member will separately be discussed after the struct definition.

![Images](c0261-01.jpg)

The `DAC_HandleTypeDef` struct members are briefly defined in the following list:

•   `DAC_TypeDef *Instance;`—This is a pointer to the DAC descriptor which will be used. For example, DAC1 is the descriptor for the first DAC peripheral.

•   `__IO HAL_DAC_StateTypeDef State;`—This value represents the DAC communication state.

•   `HAL_LockTypeDef Lock;`—This value is a DAC-locking object.

•   `DMA_HandleTypeDef *DMA_Handle1;`—This is a pointer to a DMA handler configured to perform digital-to-analog conversions in DMA mode.

•   `DMA_HandleTypeDef *DMA_Handle2;`—This is a pointer to a DMA handler configured to perform digital-to-analog conversions in DMA mode.

•   `__IO uint32_t ErrorCode;`—This is a value representing the DAC error code.

The `DAC_HandleTypeDef` struct differs from all the other similar structs in that it does not have an Init member, but instead relies on a different type of C struct to initialize the DAC at the channel level. This C sruct is named `DAC_ChannelConfTypeDef` and has the following definition. As before, each member will separately be discussed after the struct definition.

![Images](c0262-09.jpg)

The `DAC_ChannelConfTypeDef` struct members are briefly defined in the following list:

•   `uint32_t DAC_Trigger;`—This value specifies the source used to trigger the DAC conversion. This parameter can be any value of the following defines:

•   `DAC_TRIGGER_NONE`—Used for a manual trigger.

•   `DAC_TRIGGER_SOFTWARE`—Used when DAC is in a DMA mode without a timer.

•   `DAC_TRIGGER_Tx_TRGO`—Used when DAC is driven by a dedicated timer.

•   `uint32_t DAC_OutputBuffer;`—Specifies whether the DAC channel output buffer is enabled or disabled.

## Demonstration Two

In this demonstration I will be manually triggering the DAC to output a repetitive voltage ramp.

### Program Listing

The following is the code listing for this demonstration. I have also provided some additional discussions regarding pertinent code segments following the listing.

![Images](c0263-01.jpg)

![Images](c0264-01.jpg)

![Images](c0265-01.jpg)

![Images](c0266-01.jpg)

![Images](c0267-01.jpg)

![Images](c0268-01.jpg)

The significant addition to this basic code is the DAC Init function `MX_DAC_Init`. The CubeMX application generated this code when the DAC peripheral was enabled during the project creation process. There is really nothing remarkable that is happening in this function other than the output buffer is enabled and any DAC trigger is disabled.

The functional code that produces an output waveform is located in the forever loop of the main method. This code segment is relisted below to allow for an easier reference:

![Images](c0268-04.jpg)

There are two while loops within the forever loop, one which counts up and outputs a slowly increasing voltage and other counts down and outputs a slowly decreasing voltage. The waveform period is determined by the delay value, which in this demonstration has been set to 1 ms between each digital incremental value. The `HAL_DAC_SetValue` method causes the DAC to output on DAC channel 1 an analog voltage based on the 12-bit, right endian justified value for the index i.

### Test Results

[Figure 11-8](#ch11.xhtml_ch11fig8) is a screen shot from a USB oscilloscope connected to PA4, which is the DAC channel 1 output for the STM32F302R8 MCU.

![images](fig11-08.jpg)

**Figure 11-8**   *DAC output.*

You can see that it is relatively clean triangular waveform with a 1.626-ms period or an approximate frequency equal to 615 Hz. The peak-to-peak amplitude varies between approximately 1.6 and 3.3 V. These particular voltages are a result of using the values 2000 and 4000 as the DAC input limits, respectively.

I am reasonably sure that you can also increase the waveform frequency by decreasing the delay in the code as described above. Readers should try experimenting to determine the ultimate frequency limit.

## Demonstration Three

In this last demonstration I will be operating the DAC in a DMA mode to output a sine wave that is synthesized by the application. Generating an analog signal is a common task assigned to a DAC. DMA is the preferred operational method because it frees up the core processor to attend to higher priority tasks rather than focusing on generating binary input for the DAC. The following generalized statement both starts the DAC and performs a DMA data transfer from memory to the peripheral:

![Images](c0269-01.jpg)

In this demonstration, only one DAC channel named `DAC_CHANNEL_1` is available. The argument uint32_t* pData is a data pointer, which in this case will point to the beginning of the 200 element SINE array. The uint32_t Length argument is the number of data elements to be transferred, which is the NSAMP constant with value 200\. Finally, the uint32_t Alignment argument specifies the data element bit size and whether the data is right or left justified. In this case, the define `DAC_ALIGN_12B_R` shows the data is 12-bit and is aligned to the right, meaning that the least significant data bit is also the rightmost bit.

Synthesizing a sine wave requires setting the number of increments or steps that will go into making up a single cycle waveform. In this example, the number was set at 200, which is a good trade-off between having a representative sample and minimizing the total steps that need to be constantly handled. The resulting equation used to synthesize a 12-bit sine wave is as follows:

![Images](c0270-05.jpg)

This equation was used to synthesize a single sine wave cycle with the `i` step ranging from 0 to 199.

I next arbitrarily selected a period of 15 ms for the DAC sine wave output or an equivalent frequency of 66.67 Hz. This means that the conversion rate must be set at 66.67 * 200 or 13,334.

The timer TIM6 is used as trigger for the DAC’s TRGO line and its period must then be set to 13,334\. The high-speed external clock (HSE) input into TIM6 was set at 64 MHz with no prescaling. This all means the timer period value must be set to 64 MHz/13.33 KHz or approximately 4800. The actual period value was set at 4799 to account for the added 1 that goes into to the timer frequency calculation.

### Program Listing

The following is the code listing for this demonstration. I have also provided some additional discussions regarding pertinent code segments following the listing.

![Images](c0270-04.jpg)

![Images](c0271-01.jpg)

![Images](c0272-01.jpg)

![Images](c0273-01.jpg)

![Images](c0274-01.jpg)

![Images](c0275-01.jpg)

![Images](c0276-01.jpg)

### Test Results

[Figure 11-9](#ch11.xhtml_ch11fig9) is a screen shot from a USB oscilloscope connected to PA4, which is the DAC channel 1 output for the STM32F302R8 MCU.

![images](fig11-09.jpg)

**Figure 11-9**   *DAC output.*

You can see that it is a relatively clean sine waveform with a 15-ms period or an approximate frequency equal to 66.67 Hz. The peak-to-peak amplitude varies between approximately 0 and 3.3 V. This waveform is exactly what was programmed.

[Figure 11-10](#ch11.xhtml_ch11fig10) is an averaged spectrum display, which shows the main frequency components in the DAC sine wave output signal.

![images](fig11-10.jpg)

**Figure 11-10**   *Sine wave spectrum display.*

The average total harmonic distortion (THD) was measured at only 1.372%, which is very low for this type of signal generation. The third harmonic at 200 Hz was the highest distortion component and was measured at –42 dBu, which is less than one-hundredth of the primary frequency’s amplitude.

I also experimented by changing the timer TIM6 period to determine the highest possible output frequency. I determined that a minimum period value of 105 created a sine wave frequency slightly over 3 kHz. Any value lower than that period value simply caused the DAC to remain at steady high level.

The last point I will make, which is the same one that I have often repeated, is that the core Cortex-M processor is not involved with this signal generation once it has been configured, initialized, and started. Notice that the forever loop in the main method is completely devoid of any functional code because the signal generation is completely being accomplished by a combination of hardware and firmware. This approach is the essence of efficient and effective embedded design.

### Summary

This is a combination chapter that explains both direct memory access (DMA) and the digital-to-analog converter (DAC). I chose this combination because the DAC is an ideal peripheral to use with DMA operations.

The first section explains the theory behind DMA and how a DMA controller effectively implements this operational mode.

The next discussion focuses on how to use the HAL framework to both configure and initialize the MCU for DMA operations. I presented a detailed discussion concerning two C structs that are critical for setting up the DMA mode.

The first demonstration simply has the USART2 peripheral sending a character string to memory using the DMA mode. A complete program listing was provided with all the important details concerning DMA operations highlighted.

The next section introduces the DAC and provides a brief background on how it functions. This is followed by a section on how to use the HAL framework to configure and initialize this peripheral.

The second demonstration illustrates how to have the DAC generate a triangular waveform using functional code placed in the main method’s forever loop. This demonstration was purposefully designed to be computationally “heavy” in anticipation of the next demonstration.

The third and final demonstration shows how the DAC could generate a relatively “pure” sine wave using a DMA mode and then being periodically triggered by a timer. The initial signal was set at a 66-Hz frequency, but I eventually was able to generate sine wave signals slightly exceeding 3 kHz. The signal waveforms were generated without any core processor involvement other than the initial configuration.

## INDEX

*Please note that index links point to page beginnings from the print edition. Locations are approximate in e-readers, and you may need to page down one or more times after clicking a link to get to the indexed material*.

/ /, [96](#ch4.xhtml_page_96)

/* ... */, [96](#ch4.xhtml_page_96)

#, [96](#ch4.xhtml_page_96)

{ }, [96](#ch4.xhtml_page_96), [97](#ch4.xhtml_page_97)

0-ohm resistors, [8](#ch1.xhtml_page_8)

0x, [103](#ch5.xhtml_page_103)

0x0, [148](#ch7.xhtml_page_148)

0xffff, [148](#ch7.xhtml_page_148)

0xffff ffff, [148](#ch7.xhtml_page_148)

3.3-V external power supply input, [26](#ch1.xhtml_page_26), [26](#ch1.xhtml_page_26)t

10x high impedance probe settings, [127](#ch5.xhtml_page_127)

19.4-MHz bandwidth, [127](#ch5.xhtml_page_127)

32-bit STM address range, [103](#ch5.xhtml_page_103), [104](#ch5.xhtml_page_104)f

50% duty cycle waveform, [227](#ch10.xhtml_page_227)–228, [229](#ch10.xhtml_page_229)t

70-MHz bandwidth, [127](#ch5.xhtml_page_127)

acknowledgment instruction, [133](#ch6.xhtml_page_133)

ADC. *See* analog-to-digital converter (ADC)

ADC clock speed, [194](#ch9.xhtml_page_194)

ADC conversion modes, [197](#ch9.xhtml_page_197)–198

ADC resolution, [194](#ch9.xhtml_page_194)

ADC_CHANNEL_0 to ADC_CHANNEL_15, [199](#ch9.xhtml_page_199)–200

`ADC_ChannelConfTypeDef` [199](#ch9.xhtml_page_199)

ADC_CHANNEL_VBAT, [199](#ch9.xhtml_page_199)–200

ADC_CHANNEL_VREFINT, [199](#ch9.xhtml_page_199)–200

ADC_CLOCK_PCLK DIV1, [194](#ch9.xhtml_page_194)

ADC_CLOCK_PCLK DIV2, [194](#ch9.xhtml_page_194)

ADC_CLOCK_PCLK DIV4, [194](#ch9.xhtml_page_194)

ADC_CLOCK_PCLK DIV6, [194](#ch9.xhtml_page_194)

ADC_CLOCK_PCLK DIV8, [194](#ch9.xhtml_page_194)

ADC_DATAALIGN_LEFT, [194](#ch9.xhtml_page_194)

ADC_DATAALIGN_RIGHT, [194](#ch9.xhtml_page_194)

ADC_EOC_SEQ_CONV, [195](#ch9.xhtml_page_195)

ADC_EOC_SINGLE_CONV, [195](#ch9.xhtml_page_195)

ADC_EXTERNALTRIGCONVEDGE_FALLING, [196](#ch9.xhtml_page_196)

ADC_EXTERNALTRIGCONVEDGE_NONE, [196](#ch9.xhtml_page_196)

ADC_EXTERNALTRIGCONVEDGE_RISING, [196](#ch9.xhtml_page_196)

ADC_EXTERNALTRIGCONVEDGE_RISINGFALLING, [196](#ch9.xhtml_page_196)

ADC_EXTERNALTRIGCONV_EXT_IT11, [196](#ch9.xhtml_page_196)

ADC_EXTERNALTRIGCONV_T1_CC1, [196](#ch9.xhtml_page_196)

ADC_EXTERNALTRIGCONV_T1_CC2, [196](#ch9.xhtml_page_196)

ADC_EXTERNALTRIGCONV_T1_CC3, [196](#ch9.xhtml_page_196)

ADC_EXTERNALTRIGCONV_T2_CC2, [196](#ch9.xhtml_page_196)

ADC_EXTERNALTRIGCONV_T3_CC4, [196](#ch9.xhtml_page_196)

ADC_EXTERNALTRIGCONV_T4_CC4, [196](#ch9.xhtml_page_196)

ADC_EXTERNALTRIGCONV_T1_TRGO, [196](#ch9.xhtml_page_196)

ADC_EXTERNALTRIGCONV_T1_TRGO2, [196](#ch9.xhtml_page_196)

ADC_EXTERNALTRIGCONV_T2_TRGO, [196](#ch9.xhtml_page_196)

ADC_EXTERNALTRIGCONV_T4_TRGO, [196](#ch9.xhtml_page_196)

ADC_EXTERNALTRIGCONV_T5_TRGO, [196](#ch9.xhtml_page_196)

ADC_EXTERNALTRIGCONV_T6_TRGO, [196](#ch9.xhtml_page_196)

ADC_EXTERNALTRIGCONV_T8_TRGO, [196](#ch9.xhtml_page_196)

ADC_EXTERNALTRIGCONV_T8_TRGO2, [196](#ch9.xhtml_page_196)

`ADC_HandleTypeDef`, [192](#ch9.xhtml_page_192)–193

`ADC_InitTypeDef` C struct, [193](#ch9.xhtml_page_193)–194

`ADC_InitTypeDef Init`, [192](#ch9.xhtml_page_192), [193](#ch9.xhtml_page_193)

ADC_REGULAR_RANK_1 to ADC_REGULAR_RANK_16, [199](#ch9.xhtml_page_199)–200

ADC_RESOLUTION_6B, [194](#ch9.xhtml_page_194)

ADC_RESOLUTION_12B, [194](#ch9.xhtml_page_194)

ADC_SAMPLINGTIME_3CYCLES, [200](#ch9.xhtml_page_200)

ADC_SAMPLINGTIME_15CYCLES, [200](#ch9.xhtml_page_200)

ADC_SAMPLINGTIME_28CYCLES, [200](#ch9.xhtml_page_200)

ADC_SAMPLINGTIME_56CYCLES, [200](#ch9.xhtml_page_200)

ADC_SAMPLINGTIME_84CYCLES, [200](#ch9.xhtml_page_200)

ADC_SAMPLINGTIME_112CYCLES, [200](#ch9.xhtml_page_200)

ADC_SAMPLINGTIME_144CYCLES, [200](#ch9.xhtml_page_200)

ADC_SAMPLINGTIME_480CYCLES, [200](#ch9.xhtml_page_200)

ADC_SCAN_DISABLE, [194](#ch9.xhtml_page_194)

ADC_SCAN_ENABLE, [194](#ch9.xhtml_page_194)

ADC_SOFTWARE START, [196](#ch9.xhtml_page_196)

`ADC_TypeDef *Instance,` [192](#ch9.xhtml_page_192), [193](#ch9.xhtml_page_193)

advanced control timer (TIM1), [17](#ch1.xhtml_page_17), [17](#ch1.xhtml_page_17)t, [146](#ch7.xhtml_page_146), [147](#ch7.xhtml_page_147)t

AdvancedInit, [170](#ch8.xhtml_page_170)

AHB, [244](#ch11.xhtml_page_244)f

AHB1, [101](#ch5.xhtml_page_101), [106](#ch5.xhtml_page_106)f

AHB2, [106](#ch5.xhtml_page_106)f

AHB3, [106](#ch5.xhtml_page_106)f

aliased memory, [105](#ch5.xhtml_page_105)t

Analog Devices TMP36 temperature sensor, [189](#ch9.xhtml_page_189), [190](#ch9.xhtml_page_190)f, [202](#ch9.xhtml_page_202)–205

analog servo, [235](#ch10.xhtml_page_235)–236, [236](#ch10.xhtml_page_236)f

analog-to-digital conversion, [189](#ch9.xhtml_page_189)–212

ADC, [16](#ch1.xhtml_page_16), [189](#ch9.xhtml_page_189)

ADC clock speed, [194](#ch9.xhtml_page_194)

ADC conversion modes, [197](#ch9.xhtml_page_197)–198

ADC functions, [190](#ch9.xhtml_page_190)–192

ADC resolution, [194](#ch9.xhtml_page_194)

channels, groups, and ranks, [198](#ch9.xhtml_page_198)–200

demonstration program, [200](#ch9.xhtml_page_200)–212

discontinuous/continuous mode, [195](#ch9.xhtml_page_195)

DMA requests, [196](#ch9.xhtml_page_196)

end of conversion (EOC), [195](#ch9.xhtml_page_195)

group, [198](#ch9.xhtml_page_198)

HAL framework, [192](#ch9.xhtml_page_192)–197

multi-channel scan/ continuous conversion, [198](#ch9.xhtml_page_198)

multi-channel scan/single conversion, [197](#ch9.xhtml_page_197)–198, [198](#ch9.xhtml_page_198)f

polling, [200](#ch9.xhtml_page_200), [201](#ch9.xhtml_page_201)

rank, [199](#ch9.xhtml_page_199), [199](#ch9.xhtml_page_199)f

single channel/continuous conversion, [198](#ch9.xhtml_page_198)

single channel/single conversion, [197](#ch9.xhtml_page_197), [197](#ch9.xhtml_page_197)f

successive-approximation register (SAR), [190](#ch9.xhtml_page_190), [191](#ch9.xhtml_page_191)f

TMP36 temperature sensor, [189](#ch9.xhtml_page_189), [190](#ch9.xhtml_page_190)f, [202](#ch9.xhtml_page_202)–205

analog-to-digital converter (ADC), [16](#ch1.xhtml_page_16), [189](#ch9.xhtml_page_189)

analog voltage outputs, [260](#ch11.xhtml_page_260), [260](#ch11.xhtml_page_260)t, [261](#ch11.xhtml_page_261)f

analog voltage reference (AREF), [12](#ch1.xhtml_page_12)

APB1 peripheral allocations, [107](#ch5.xhtml_page_107), [108](#ch5.xhtml_page_108)f

APB2, [106](#ch5.xhtml_page_106)f

Application/MDK-ARM, [70](#ch3.xhtml_page_70)f, [80](#ch3.xhtml_page_80)

Application/User, [70](#ch3.xhtml_page_70)f, [80](#ch3.xhtml_page_80)

Arduino connectors, [10](#ch1.xhtml_page_10)–12, [114](#ch5.xhtml_page_114)f

Arduino IDE, [32](#ch2.xhtml_page_32)

Arduino prototype board, [112](#ch5.xhtml_page_112), [114](#ch5.xhtml_page_114)f

AREF. *See* analog voltage reference (AREF)

ARM, [78](#ch3.xhtml_page_78)

ARM Cortex M-4 block diagram, [5](#ch1.xhtml_page_5)f

ARM Cortex Microcontroller Interface Standard (CMSIS), [78](#ch3.xhtml_page_78)–85

axf format, [82](#ch3.xhtml_page_82)

Build process log, [81](#ch3.xhtml_page_81), [81](#ch3.xhtml_page_81)f

compiling and downloading the project, [80](#ch3.xhtml_page_80)–82

components, [79](#ch3.xhtml_page_79)

CubeMX-generated C code, [80](#ch3.xhtml_page_80), [80](#ch3.xhtml_page_80)f

downloading the hex code, [82](#ch3.xhtml_page_82)–86

Keil IDE build icon, [81](#ch3.xhtml_page_81), [81](#ch3.xhtml_page_81)f

ST-LINK, [82](#ch3.xhtml_page_82)–86

arming/disarming, [131](#ch6.xhtml_page_131)

asynchronous event, [129](#ch6.xhtml_page_129)

axf format, [82](#ch3.xhtml_page_82)

B1 USER, [22](#ch1.xhtml_page_22)

B2 RESET, [22](#ch1.xhtml_page_22)

background thread/foreground thread, [132](#ch6.xhtml_page_132)

Bare metal development, [30](#ch2.xhtml_page_30)

BASEPRI register, [131](#ch6.xhtml_page_131)–132

basic timer (TIM6), [17](#ch1.xhtml_page_17)t, [18](#ch1.xhtml_page_18), [146](#ch7.xhtml_page_146), [147](#ch7.xhtml_page_147)t

baud rate chart, [171](#ch8.xhtml_page_171)f

Baudrate, [171](#ch8.xhtml_page_171)

binary code, [34](#ch2.xhtml_page_34)

binary divider (prescaler), [145](#ch7.xhtml_page_145), [147](#ch7.xhtml_page_147)–148

bit serial communications, [167](#ch8.xhtml_page_167)–188

clear-to-send (CTS) line, [169](#ch8.xhtml_page_169)

data transfer protocol, [168](#ch8.xhtml_page_168)–169, [188](#ch8.xhtml_page_188)

enabling USART2, [175](#ch8.xhtml_page_175)–176

full-duplex communications, [168](#ch8.xhtml_page_168), [169](#ch8.xhtml_page_169)f

protocol control lines, [168](#ch8.xhtml_page_168)–169

Realterm terminal program, [172](#ch8.xhtml_page_172)–175

request/acknowledge, [169](#ch8.xhtml_page_169)

request-to-send (RTS) line, [169](#ch8.xhtml_page_169)

UART block diagram, [167](#ch8.xhtml_page_167)f

UART vs. USART, [167](#ch8.xhtml_page_167), [168](#ch8.xhtml_page_168)

USART block diagram, [168](#ch8.xhtml_page_168)f

USART configuration, [170](#ch8.xhtml_page_170)–172

USART2 global interrupt, [182](#ch8.xhtml_page_182)

USART receive demonstration program, [182](#ch8.xhtml_page_182)–188

USART transmit demonstration program, [176](#ch8.xhtml_page_176)–181

Windows terminal program, [172](#ch8.xhtml_page_172)–175

bit serial ports, [19](#ch1.xhtml_page_19)–21

I2C, [19](#ch1.xhtml_page_19)–20

I2S, [21](#ch1.xhtml_page_21)

SPI, [20](#ch1.xhtml_page_20)–21

USART, [19](#ch1.xhtml_page_19)

Board Selector dialog screen shot, [55](#ch3.xhtml_page_55), [57](#ch3.xhtml_page_57)f

BOOT, [58](#ch3.xhtml_page_58)f, [59](#ch3.xhtml_page_59)

BOOT0 input pin, [13](#ch1.xhtml_page_13)

braces { }, [96](#ch4.xhtml_page_96), [97](#ch4.xhtml_page_97)

buffer output amplifier, [260](#ch11.xhtml_page_260)

bugs, [34](#ch2.xhtml_page_34)

Build process log, [81](#ch3.xhtml_page_81), [81](#ch3.xhtml_page_81)f

bus controller, [241](#ch11.xhtml_page_241), [244](#ch11.xhtml_page_244)

bus matrix, [244](#ch11.xhtml_page_244), [244](#ch11.xhtml_page_244)f, [245](#ch11.xhtml_page_245)

bus matrix block diagram, [244](#ch11.xhtml_page_244)f

C/C++ language projects. *See* STM project development

CCRx register. *See* compare capture registers (CCRx)

CIE1931 lightness formula, [231](#ch10.xhtml_page_231)

clear-to-send (CTS) line, [169](#ch8.xhtml_page_169)

Clock Configuration gui, [62](#ch3.xhtml_page_62)f

Clock Configuration tab, [62](#ch3.xhtml_page_62)–63

clock skew, [124](#ch5.xhtml_page_124)–125, [128](#ch5.xhtml_page_128)

clock speed, [124](#ch5.xhtml_page_124)

clock speed demonstration, [124](#ch5.xhtml_page_124)–127

ClockDivision, [148](#ch7.xhtml_page_148)

CMSIS. *See* ARM Cortex Microcontroller Interface Standard (CMSIS)

CMSIS-CORE, [79](#ch3.xhtml_page_79)

CMSIS-DAP, [79](#ch3.xhtml_page_79)

CMSIS-Driver, [79](#ch3.xhtml_page_79)

CMSIS-DSP, [79](#ch3.xhtml_page_79)

CMSIS-Pack, [79](#ch3.xhtml_page_79)

CMSIS-RTOS, [79](#ch3.xhtml_page_79)

CMSIS-SVD, [79](#ch3.xhtml_page_79)

CN5 connector pinout, [11](#ch1.xhtml_page_11), [12](#ch1.xhtml_page_12)t

CN6 connector pinout, [10](#ch1.xhtml_page_10)f, [11](#ch1.xhtml_page_11)t

CN7 connector pinout, [13](#ch1.xhtml_page_13), [13](#ch1.xhtml_page_13)t

CN8 connector pinout, [11](#ch1.xhtml_page_11), [11](#ch1.xhtml_page_11)t

CN9 connector pinout, [12](#ch1.xhtml_page_12), [12](#ch1.xhtml_page_12)t

CN10 connector pinout, [13](#ch1.xhtml_page_13), [13](#ch1.xhtml_page_13)t

CNT counter, [216](#ch10.xhtml_page_216), [217](#ch10.xhtml_page_217)f

Code Generation dialog box, [68](#ch3.xhtml_page_68), [69](#ch3.xhtml_page_69)f

Code Generator screen, [68](#ch3.xhtml_page_68), [69](#ch3.xhtml_page_69)f

coding trade-off (simpler code vs. compact, complex code), [165](#ch7.xhtml_page_165)

comments, [96](#ch4.xhtml_page_96)

commercial proprietary software, [29](#ch2.xhtml_page_29)–30

COMPARATOR module, [191](#ch9.xhtml_page_191), [191](#ch9.xhtml_page_191)f

compare capture registers (CCRx), [214](#ch10.xhtml_page_214), [216](#ch10.xhtml_page_216), [217](#ch10.xhtml_page_217)f

complete [32](#ch2.xhtml_page_32)-bit STM address range, [103](#ch5.xhtml_page_103), [104](#ch5.xhtml_page_104)f

Configuration View icons, [64](#ch3.xhtml_page_64)f

Configuration View tab, [63](#ch3.xhtml_page_63)–64

Configure Flash Tools, [82](#ch3.xhtml_page_82)

context switch, [132](#ch6.xhtml_page_132)

core memory address ranges, [105](#ch5.xhtml_page_105)t

core memory addresses, [103](#ch5.xhtml_page_103)–105

Cortex M-4 processor, [4](#ch1.xhtml_page_4), [5](#ch1.xhtml_page_5)f

Cortex Microcontroller Interface Standard (CMSIS). *See* ARM Cortex Microcontroller Interface Standard (CMSIS)

CounterMode, [148](#ch7.xhtml_page_148)

counters, [16](#ch1.xhtml_page_16)–19\. *See also* timers

cross-compiler, [30](#ch2.xhtml_page_30), [34](#ch2.xhtml_page_34)

CTS. *See* clear-to-send (CTS) line

CubeMX, [37](#ch2.xhtml_page_37)–40, [53](#ch3.xhtml_page_53)–86

ARM CMSIS. *See* ARM Cortex Microcontroller Interface Standard (CMSIS)

Board Selector dialog screen shot, [55](#ch3.xhtml_page_55), [57](#ch3.xhtml_page_57)f

Clock Configuration tab, [62](#ch3.xhtml_page_62)–63

Configuration View tab, [63](#ch3.xhtml_page_63)–64

features, [53](#ch3.xhtml_page_53)–54

Help document, [54](#ch3.xhtml_page_54)–55, [56](#ch3.xhtml_page_56)f

IP tree pane, [61](#ch3.xhtml_page_61)–62

Load Project, [54](#ch3.xhtml_page_54), [55](#ch3.xhtml_page_55)f

MCU alternative functions, [60](#ch3.xhtml_page_60)–61

MCU-centric utility, [53](#ch3.xhtml_page_53)

New Project. *See* New Project (CubeMX)

NUCLEO-F302R8 board selection, [55](#ch3.xhtml_page_55), [57](#ch3.xhtml_page_57)f

opening screen, [37](#ch2.xhtml_page_37)f, [54](#ch3.xhtml_page_54)f

PC13 alternative pin mappings, [60](#ch3.xhtml_page_60)f

Pinout tab, [58](#ch3.xhtml_page_58)–60

Power Consumption Calculator View tab, [65](#ch3.xhtml_page_65)

purpose, [86](#ch3.xhtml_page_86)

RCC pin configurations, [63](#ch3.xhtml_page_63)

DAC. *See* digital-to-analog converter (DAC)

DAC clock source. *See* digital-to-analog converter (DAC) clock source

DAC_ALIGN_12B_R, [270](#ch11.xhtml_page_270)

`DAC_ChannelConfTypeDef`, [262](#ch11.xhtml_page_262)

`DAC_HandleTypeDef`, [261](#ch11.xhtml_page_261)

DAC_TRIGGER_NONE, [262](#ch11.xhtml_page_262)

DAC_TRIGGER_SOFTWARE, [262](#ch11.xhtml_page_262)

DAC_TRIGGER_Tx_TRGO, [262](#ch11.xhtml_page_262)

`DAC_TypeDef *Instance`, [261](#ch11.xhtml_page_261)

daemon, [44](#ch2.xhtml_page_44)

DAP. *See* debug access port (DAP)

data transfer, [241](#ch11.xhtml_page_241)

data transfer concepts, [242](#ch11.xhtml_page_242)–245

data transfer process, [241](#ch11.xhtml_page_241)

data transfer protocol, [168](#ch8.xhtml_page_168)–169, [188](#ch8.xhtml_page_188)

dead time generator, [146](#ch7.xhtml_page_146)

dead time insertions, [146](#ch7.xhtml_page_146)

debug access port (DAP), [79](#ch3.xhtml_page_79)

debugging, [34](#ch2.xhtml_page_34)

debugging tool. *See* OpenOCD15

decrementing counter, [145](#ch7.xhtml_page_145)

define statements, [99](#ch4.xhtml_page_99), [122](#ch5.xhtml_page_122)

*Definitive Guide to ARM Cortex-M3 and Cortex-M4 Processors* (Yiu), [4](#ch1.xhtml_page_4)

Device Database menu selection, [71](#ch3.xhtml_page_71), [71](#ch3.xhtml_page_71)f

Device not found dialog box, [71](#ch3.xhtml_page_71), [71](#ch3.xhtml_page_71)f

Dhrystone million instructions per second (DMIPS), [65](#ch3.xhtml_page_65)

digital-to-analog converter (DAC), [241](#ch11.xhtml_page_241), [259](#ch11.xhtml_page_259)–278

analog voltage outputs, [260](#ch11.xhtml_page_260), [260](#ch11.xhtml_page_260)t, [261](#ch11.xhtml_page_261)f

buffer output amplifier, [260](#ch11.xhtml_page_260)

HAL framework, [261](#ch11.xhtml_page_261)–262

noise, [260](#ch11.xhtml_page_260)

R-2R resistor ladder network, [259](#ch11.xhtml_page_259), [259](#ch11.xhtml_page_259)f

sine wave signals, [269](#ch11.xhtml_page_269)–278

triangular waveform, [263](#ch11.xhtml_page_263)–269

digital-to-analog converter (DAC) clock source, [146](#ch7.xhtml_page_146)

direct memory access (DMA), [241](#ch11.xhtml_page_241)–258

analogy (bypass highway), [243](#ch11.xhtml_page_243)

bus controller, [241](#ch11.xhtml_page_241), [244](#ch11.xhtml_page_244)

bus matrix, [244](#ch11.xhtml_page_244), [244](#ch11.xhtml_page_244)f, [245](#ch11.xhtml_page_245)

data transfer concepts, [242](#ch11.xhtml_page_242)–245

DMA block diagram, [242](#ch11.xhtml_page_242)f

DMA channels, [245](#ch11.xhtml_page_245), [247](#ch11.xhtml_page_247)f

DMA controller details, [245](#ch11.xhtml_page_245)–246

final steps in setting up DMA transfer, [250](#ch11.xhtml_page_250)–251

HAL framework, [246](#ch11.xhtml_page_246)–250

memory port, [245](#ch11.xhtml_page_245)

peripheral port, [245](#ch11.xhtml_page_245)

priority assignment hardware unit, [245](#ch11.xhtml_page_245)

Round Robin algorithm, [244](#ch11.xhtml_page_244)

slave port, [245](#ch11.xhtml_page_245)

software triggering, [245](#ch11.xhtml_page_245)

USART2 sending character string to memory, [251](#ch11.xhtml_page_251)–258

direct X1 probe settings, [127](#ch5.xhtml_page_127)

`DisableInterrupts ( )` [131](#ch6.xhtml_page_131)

disclaimer, [72](#ch3.xhtml_page_72), [73](#ch3.xhtml_page_73)f

DMA. *See* direct memory access (DMA)

DMA block diagram, [242](#ch11.xhtml_page_242)f

DMA channel block diagram, [247](#ch11.xhtml_page_247)f

DMA channels, [245](#ch11.xhtml_page_245), [247](#ch11.xhtml_page_247)f

`DMA_Channel_TypeDef *Instance`, [246](#ch11.xhtml_page_246)

DMA_CIRCULAR, [250](#ch11.xhtml_page_250)

`DMA_HandleTypeDef`, [246](#ch11.xhtml_page_246)

`DMA_HandleTypeDef *DMA_Handle`, [192](#ch9.xhtml_page_192), [193](#ch9.xhtml_page_193)

`DMA_HandleTypeDef *DMA_Handle1` [261](#ch11.xhtml_page_261), [262](#ch11.xhtml_page_262)

`DMA_HandleTypeDef *DMA_Handle2` [261](#ch11.xhtml_page_261), [262](#ch11.xhtml_page_262)

`DMA_InitTypeDef`, [248](#ch11.xhtml_page_248)

`DMA_InitTypeDef Init`, [246](#ch11.xhtml_page_246), [248](#ch11.xhtml_page_248)

DMA_MDATAALIGN_BYTE, [249](#ch11.xhtml_page_249)

DMA_MDATAALIGN_HALFWORD, [249](#ch11.xhtml_page_249)

DMA_MDATAALIGN_WORD, [249](#ch11.xhtml_page_249)

DMA_MEMORY_TO_MEMORY, [249](#ch11.xhtml_page_249)

DMA_MEMORY_TO_PERIPH, [249](#ch11.xhtml_page_249)

DMA_NORMAL, [250](#ch11.xhtml_page_250)

DMA_PDATAALIGN_BYTE, [249](#ch11.xhtml_page_249)

DMA_PDATAALIGN_HALFWORD, [249](#ch11.xhtml_page_249)

DMA_PDATAALIGN_WORD, [249](#ch11.xhtml_page_249)

DMA_PERIPH_TO_MEMORY, [249](#ch11.xhtml_page_249)

DMA_PINC_DISABLE, [249](#ch11.xhtml_page_249)

DMA_PINC_ENABLE, [249](#ch11.xhtml_page_249)

DMA_PRIORITY_HIGH, [250](#ch11.xhtml_page_250)

DMA_PRIORITY_LOW, [250](#ch11.xhtml_page_250)

DMA_PRIORITY_MEDIUM, [250](#ch11.xhtml_page_250)

DMA_PRIORITY_VERY_HIGH, [250](#ch11.xhtml_page_250)

DMIPS. *See* Dhrystone million instructions per second (DMIPS)

Drivers/CMSIS, [70](#ch3.xhtml_page_70)f, [80](#ch3.xhtml_page_80)

Drivers/STM32F3xx_HAL_Driver, [70](#ch3.xhtml_page_70)f, [80](#ch3.xhtml_page_80)

duty cycle, [214](#ch10.xhtml_page_214)

EEPROM, [31](#ch2.xhtml_page_31)

`EnableInterrupts ( )`, [131](#ch6.xhtml_page_131)

en.stsw-link004, [41](#ch2.xhtml_page_41)

en.stsw-link009, [41](#ch2.xhtml_page_41)

error dialog, [90](#ch4.xhtml_page_90)–91, [92](#ch4.xhtml_page_92)f

E5V external power supply, [25](#ch1.xhtml_page_25), [25](#ch1.xhtml_page_25)t, [26](#ch1.xhtml_page_26)

exceptions, [129](#ch6.xhtml_page_129). *See also* interrupt

external interrupt, [134](#ch6.xhtml_page_134)–135

external interrupt controller (EXTI), [16](#ch1.xhtml_page_16), [134](#ch6.xhtml_page_134)

external power supply output, [26](#ch1.xhtml_page_26)

EXTI. *See* external interrupt controller (EXTI)

EXTI block diagram, [135](#ch6.xhtml_page_135)f

EXTI line [15:10] interrupt, [143](#ch6.xhtml_page_143)

EXTI15_10_IRQ, [135](#ch6.xhtml_page_135)

first microcontroller (TMS1000), [30](#ch2.xhtml_page_30)

flash memory, [105](#ch5.xhtml_page_105)t

floating, [111](#ch5.xhtml_page_111)

floating point unit (FPU), [132](#ch6.xhtml_page_132)

forever loop, [78](#ch3.xhtml_page_78), [97](#ch4.xhtml_page_97), [98](#ch4.xhtml_page_98)

FPU. *See* floating point unit (FPU)

full-duplex communications, [168](#ch8.xhtml_page_168), [169](#ch8.xhtml_page_169)f

GDB. *See* GNU Project Debugger (GDB)

general purpose (GP) timers, [17](#ch1.xhtml_page_17)–18, [17](#ch1.xhtml_page_17)t, [146](#ch7.xhtml_page_146), [147](#ch7.xhtml_page_147)t

general purpose input-output (GPIO), [16](#ch1.xhtml_page_16)

CubeMX, [58](#ch3.xhtml_page_58)–60

HAL. *See* GPIO pins and hardware abstract layer (HAL)

interrupt, [134](#ch6.xhtml_page_134)–135, [136](#ch6.xhtml_page_136)f

general-purpose timer PWM signal generation, [214](#ch10.xhtml_page_214)–216

generic toolchain workflow, [33](#ch2.xhtml_page_33)f, [34](#ch2.xhtml_page_34)

GNU Project Debugger (GDB), [44](#ch2.xhtml_page_44)–45

gnuarmeclipse-openocd-win64-0.10.0-201701241841-setup.exe, [43](#ch2.xhtml_page_43), [44](#ch2.xhtml_page_44)f

GP timer. *See* general purpose (GP) timers

GPIO. *See* general purpose input-output (GPIO)

GPIO clock speed, [124](#ch5.xhtml_page_124)–127

`GPIO_InitStruct.Mode = GPIO_MODE_IT-RISING`, [141](#ch6.xhtml_page_141)

GPIO_Instruct, [117](#ch5.xhtml_page_117)

GPIO_Instruct C data structures, [125](#ch5.xhtml_page_125)–126

GPIO_Instruct to GPIO Register Equivalence, [117](#ch5.xhtml_page_117)f

GPIO_Instruct.Mode, [117](#ch5.xhtml_page_117)f

GPIO_Instruct.Pin, [117](#ch5.xhtml_page_117)f

GPIO_Instruct.Pull, [117](#ch5.xhtml_page_117)f

GPIO_Instruct.Speed, [117](#ch5.xhtml_page_117)f

GPIO pin hardware, [109](#ch5.xhtml_page_109)–111

GPIO pin signal waveforms, [126](#ch5.xhtml_page_126), [126](#ch5.xhtml_page_126)f

GPIO pins and hardware abstract layer (HAL), [101](#ch5.xhtml_page_101)–128

core memory addresses, [103](#ch5.xhtml_page_103)–105

HAL_GPIO. *See* HAL_GPIO module

memory-mapped peripherals, [103](#ch5.xhtml_page_103)

peripheral memory addresses, [105](#ch5.xhtml_page_105)–108

GPIO port mode register, [111](#ch5.xhtml_page_111)f

GPIO port pin block diagram/schematic, [109](#ch5.xhtml_page_109)f

GPIO registers, [111](#ch5.xhtml_page_111), [112](#ch5.xhtml_page_112)f, [113](#ch5.xhtml_page_113)f

GPIO signal skew, [124](#ch5.xhtml_page_124)–125, [128](#ch5.xhtml_page_128)

GPIOA_MODER, [112](#ch5.xhtml_page_112)f

GPIOA_OSPEEDER, [112](#ch5.xhtml_page_112)f

GPIOA_PUPDR, [113](#ch5.xhtml_page_113)f

GPIOB_MODER, [112](#ch5.xhtml_page_112)f

GPIOB_OSPEEDER, [112](#ch5.xhtml_page_112)f

GPIOB_PUPDR, [113](#ch5.xhtml_page_113)f

GPIOx_AFRH, [113](#ch5.xhtml_page_113)f

GPIOx_AFRL, [113](#ch5.xhtml_page_113)f

GPIOx_BSRR, [113](#ch5.xhtml_page_113)f

GPIOx_IDR, [113](#ch5.xhtml_page_113)f

GPIOx_LCKR, [113](#ch5.xhtml_page_113)f

GPIOx_MODER, [110](#ch5.xhtml_page_110), [112](#ch5.xhtml_page_112)f, [117](#ch5.xhtml_page_117)f

GPIOx_ODR, [113](#ch5.xhtml_page_113)f

GPIOx_OSPEEDER, [112](#ch5.xhtml_page_112)f, [117](#ch5.xhtml_page_117)f

GPIOx_OTYPER, [112](#ch5.xhtml_page_112)f, [117](#ch5.xhtml_page_117)f

GPIOx_PUPDR, [113](#ch5.xhtml_page_113)f, [117](#ch5.xhtml_page_117)f

group, [198](#ch9.xhtml_page_198)

HAL. *See* GPIO pins and hardware abstract layer (HAL); HAL framework

HAL framework

analog-to-digital conversion, [192](#ch9.xhtml_page_192)–197

digital-to-analog converter (DAC), [261](#ch11.xhtml_page_261)–262

direct memory access (DMA), [246](#ch11.xhtml_page_246)–250

pulse-width modulation (PWM), [216](#ch10.xhtml_page_216)–220

`HAL_ADC_Init( )`, [201](#ch9.xhtml_page_201)

`HAL_ADC_PollForConversion (&hadcl,` [`100`](#ch4.xhtml_page_100)`)`, [206](#ch9.xhtml_page_206)

`HAL_ADC_Start ( )`, [201](#ch9.xhtml_page_201)

`HAL_ADC_Start (&hadc1)`, [206](#ch9.xhtml_page_206)

`HAL_ADC_Stop ( )`, [201](#ch9.xhtml_page_201)

`HAL_DAC_SetValue`, [268](#ch11.xhtml_page_268)

`HAL_Delay` [`200`](#ch9.xhtml_page_200), [180](#ch8.xhtml_page_180), [181](#ch8.xhtml_page_181)

`HAL_Delay 500`, [98](#ch4.xhtml_page_98), [99](#ch4.xhtml_page_99)

`HAL_Delay 1000`, [206](#ch9.xhtml_page_206), [207](#ch9.xhtml_page_207)

`HAL_DMA_IRQHandler ( )`, [248](#ch11.xhtml_page_248)

HAL_GPIO module, [107](#ch5.xhtml_page_107)–124

clock speed demonstration, [124](#ch5.xhtml_page_124)–127

GPIO pin hardware, [109](#ch5.xhtml_page_109)–111

GPIO port mode register, [111](#ch5.xhtml_page_111)f

GPIO registers, [111](#ch5.xhtml_page_111), [112](#ch5.xhtml_page_112)f, [113](#ch5.xhtml_page_113)f

main.c code listing, [117](#ch5.xhtml_page_117)–121

modification (enabling multiple LED outputs), [122](#ch5.xhtml_page_122)–123

push button test demonstration, [123](#ch5.xhtml_page_123)–124, [128](#ch5.xhtml_page_128)

simple LED test demonstration, [111](#ch5.xhtml_page_111)–122, [128](#ch5.xhtml_page_128)

`HAL_GPIO_TogglePin (LD2_GPIO_Port, LD2_Pin)`, [98](#ch4.xhtml_page_98), [99](#ch4.xhtml_page_99)

`HAL_Init ( )`, [78](#ch3.xhtml_page_78)

`HAL_LockTypeDef Lock`, [192](#ch9.xhtml_page_192), [193](#ch9.xhtml_page_193), [246](#ch11.xhtml_page_246), [248](#ch11.xhtml_page_248), [261](#ch11.xhtml_page_261), [262](#ch11.xhtml_page_262)

`HAL_NVIC_EnableIRQ (EXTI15_10_IRQn)`, [141](#ch6.xhtml_page_141)

`HAL_NVIC_EnableIRQ (TIM2_IRQn)`, [156](#ch7.xhtml_page_156)

`HAL_NVIC_SetPriority (ETXTI15_10_IRQn, 0, 0)`, [141](#ch6.xhtml_page_141)

`HAL_NVIC_SetPriority (TIM2_IRQn, 0, 0)`, [156](#ch7.xhtml_page_156)

`HAL_StatusTypeDef_HAL_ADC_PollForConversion (ADC_Handle_TypeDef* hadc, uint32_t Timeout)`, [201](#ch9.xhtml_page_201)

`HAL_StatusTypeDef_HAL_DAC_Start_DMA (DAC_HandleTypeDef *hdac, uint32_t Channel, uint32_t* pData, uint32_t Length, uint32_t Alignment)`, [269](#ch11.xhtml_page_269)

`HAL_StatusTypeDef_HAL_DMA_Start (DMA_HandleTypeDef *hdma, uint32_t SrcAddress, uint32_t Dst Address, uint32_t DataLength)`, [250](#ch11.xhtml_page_250)

`halt` command, [51](#ch2.xhtml_page_51), [51](#ch2.xhtml_page_51)f

`HAL_TIM_Base_Start_IT (&htim2)`, [156](#ch7.xhtml_page_156)

`HAL_UART_Transmit (&huart2, (uint8_t*) msg,` [`10`](#ch1.xhtml_page_10)`,` [`100`](#ch4.xhtml_page_100)`)`, [180](#ch8.xhtml_page_180), [181](#ch8.xhtml_page_181)

`HAL_UART_Transmit (&huart2, (uint8_t*) msg,` [`20`](#ch1.xhtml_page_20)`,` [`100`](#ch4.xhtml_page_100)`)`, [206](#ch9.xhtml_page_206), [207](#ch9.xhtml_page_207)

hardware, [1](#ch1.xhtml_page_1)–28\. *See also* microcontroller (MCU); Nucleo-64 board options

hardware abstract layer. *See* GPIO pins and hardware abstract layer (HAL)

hardware timers. *See* timers

Harvard architecture, [5](#ch1.xhtml_page_5)

header file, [97](#ch4.xhtml_page_97)

Hello World program. *See* STM project development

hex code download, [82](#ch3.xhtml_page_82)–86

high-resolution timers, [146](#ch7.xhtml_page_146)

high-speed external clock (HSE), [23](#ch1.xhtml_page_23)–24, [62](#ch3.xhtml_page_62)–63, [270](#ch11.xhtml_page_270)

historical overview, [30](#ch2.xhtml_page_30)–31

Hitec model HS-311 analog servo, [236](#ch10.xhtml_page_236)f, [237](#ch10.xhtml_page_237)

hobby-grade servo motor, [235](#ch10.xhtml_page_235)–239

HRTIM1, [146](#ch7.xhtml_page_146)

HSE. *See* high-speed external clock (HSE)

human eye brightness perception, [229](#ch10.xhtml_page_229), [230](#ch10.xhtml_page_230)f

HwFlowCtl, [172](#ch8.xhtml_page_172)

I2C, [19](#ch1.xhtml_page_19)–20

I2C block diagram, [20](#ch1.xhtml_page_20)f

I2C signal lines, [20](#ch1.xhtml_page_20)f

I2S, [21](#ch1.xhtml_page_21)

I2S2, [21](#ch1.xhtml_page_21)

I2S3, [21](#ch1.xhtml_page_21)

I/O pin, [109](#ch5.xhtml_page_109), [109](#ch5.xhtml_page_109)f

IDE. *See* integrated development environment (IDE)

IDE download Web page, [36](#ch2.xhtml_page_36)f

if/else statement, [99](#ch4.xhtml_page_99), [100](#ch4.xhtml_page_100)

IN0, [198](#ch9.xhtml_page_198), [199](#ch9.xhtml_page_199)f

IN1, [198](#ch9.xhtml_page_198), [199](#ch9.xhtml_page_199)f

`#include “main.h”`, [92](#ch4.xhtml_page_92), [96](#ch4.xhtml_page_96)–97

infinite loop, [97](#ch4.xhtml_page_97). *See also* forever loop

Init, [170](#ch8.xhtml_page_170)

Instance, [170](#ch8.xhtml_page_170)

`int`, [97](#ch4.xhtml_page_97)

integrated development environment (IDE), [32](#ch2.xhtml_page_32)

integrated peripheral (IP) tree pane, [61](#ch3.xhtml_page_61)–62

Intel 805x family of MCUs, [31](#ch2.xhtml_page_31)

Intel 8048, [30](#ch2.xhtml_page_30)

Intel 8052, [31](#ch2.xhtml_page_31), [32](#ch2.xhtml_page_32)t

Intel 8751, [31](#ch2.xhtml_page_31), [31](#ch2.xhtml_page_31)f

inter-integrated circuit. *See* I2C

inter-integrated sound. *See* I2S

interrupt, [129](#ch6.xhtml_page_129)–144

acknowledgment instruction, [133](#ch6.xhtml_page_133)

arming/disarming, [131](#ch6.xhtml_page_131)

asynchronous event, [129](#ch6.xhtml_page_129)

background thread/foreground thread, [132](#ch6.xhtml_page_132)

BASEPRI register, [131](#ch6.xhtml_page_131)–132

context switch, [132](#ch6.xhtml_page_132)

defined, [14](#ch1.xhtml_page_14), [129](#ch6.xhtml_page_129)

demonstration/test run, [135](#ch6.xhtml_page_135)–144

enabling/disabling, [131](#ch6.xhtml_page_131)

external, [134](#ch6.xhtml_page_134)–135

EXTI line [15:10], [143](#ch6.xhtml_page_143)

EXTI15_10_IRQ, [135](#ch6.xhtml_page_135)

GPIO pins, external interrupt controller, and NVIC IRQs, [134](#ch6.xhtml_page_134)–135, [136](#ch6.xhtml_page_136)f

main.c file listing, [137](#ch6.xhtml_page_137)–141

maskable, [131](#ch6.xhtml_page_131)

`MX_GPIO_Init` method, [138](#ch6.xhtml_page_138), [141](#ch6.xhtml_page_141)

NVIC, [130](#ch6.xhtml_page_130)–131

overflow, [145](#ch7.xhtml_page_145)

pending interrupt request, [133](#ch6.xhtml_page_133)

polling, [133](#ch6.xhtml_page_133)–134

preconditions, [132](#ch6.xhtml_page_132)

priority level, [15](#ch1.xhtml_page_15), [131](#ch6.xhtml_page_131)

processing sequence, [132](#ch6.xhtml_page_132), [133](#ch6.xhtml_page_133)f

RCC global, [142](#ch6.xhtml_page_142)–143

stm32f3xx_it.c file listing, [142](#ch6.xhtml_page_142)

System tick timer, [142](#ch6.xhtml_page_142)

SysTick, [131](#ch6.xhtml_page_131), [133](#ch6.xhtml_page_133)

USART2 global, [182](#ch8.xhtml_page_182)

users, [129](#ch6.xhtml_page_129)

vector table, [133](#ch6.xhtml_page_133)

what happens when interrupt is recognized, [132](#ch6.xhtml_page_132), [133](#ch6.xhtml_page_133)f

interrupt channel, [130](#ch6.xhtml_page_130), [131](#ch6.xhtml_page_131)

interrupt-driven blink LED timer, [155](#ch7.xhtml_page_155)–157

interrupt flow diagram, [14](#ch1.xhtml_page_14)f

interrupt handler, [129](#ch6.xhtml_page_129)

interrupt processing sequence, [132](#ch6.xhtml_page_132), [133](#ch6.xhtml_page_133)f

interrupt request (IRQ), [15](#ch1.xhtml_page_15), [130](#ch6.xhtml_page_130), [130](#ch6.xhtml_page_130)f

interrupt service routine (ISR), [14](#ch1.xhtml_page_14), [132](#ch6.xhtml_page_132)–134, [143](#ch6.xhtml_page_143)

`_IO HAL_DAC_StateTypeDef State`, [261](#ch11.xhtml_page_261), [262](#ch11.xhtml_page_262)

`_IO HAL_DMA_StateTypeDef State`, [246](#ch11.xhtml_page_246), [248](#ch11.xhtml_page_248)

`_IO uint32_t`, [192](#ch9.xhtml_page_192), [193](#ch9.xhtml_page_193)

`_IO uint32_t ErrorCode`, [193](#ch9.xhtml_page_193), [246](#ch11.xhtml_page_246), [248](#ch11.xhtml_page_248), [261](#ch11.xhtml_page_261), [262](#ch11.xhtml_page_262)

`_IO uint32_t State`, [193](#ch9.xhtml_page_193)

I/O pin, [109](#ch5.xhtml_page_109), [109](#ch5.xhtml_page_109)f

Ionescu, Liviu, [43](#ch2.xhtml_page_43)

IOREF pin, [11](#ch1.xhtml_page_11)

IP tree pane. *See* integrated peripheral (IP) tree pane

IRQ. *See* interrupt request (IRQ)

ISR. *See* interrupt service routine (ISR)

JP1, [25](#ch1.xhtml_page_25)

JP1 configuration table, [25](#ch1.xhtml_page_25)t

JP5 jumper positions, [26](#ch1.xhtml_page_26)t

JP6, [23](#ch1.xhtml_page_23)

Keil IDE, [30](#ch2.xhtml_page_30), [32](#ch2.xhtml_page_32), [35](#ch2.xhtml_page_35)–36, [52](#ch2.xhtml_page_52), [90](#ch4.xhtml_page_90), [92](#ch4.xhtml_page_92)f

Keil IDE build icon, [81](#ch3.xhtml_page_81), [81](#ch3.xhtml_page_81)f

Keil IDE v4.74 icon, [36](#ch2.xhtml_page_36)f

Keil registration form, [35](#ch2.xhtml_page_35)f

LD1, [22](#ch1.xhtml_page_22)

LD2, [22](#ch1.xhtml_page_22)

LD3, [22](#ch1.xhtml_page_22)

leading edge delay, [124](#ch5.xhtml_page_124)

leading edge rise time, [127](#ch5.xhtml_page_127)

LED

color/luminescence of tricolor LED, [231](#ch10.xhtml_page_231)–235

interrupt-driven blink LED timer, [155](#ch7.xhtml_page_155)–157

LED states, [22](#ch1.xhtml_page_22)

linear dimming property, [231](#ch10.xhtml_page_231)

luminescence of normal LED, [228](#ch10.xhtml_page_228)–231

multi-rate interrupt-driven blink LED timer, [157](#ch7.xhtml_page_157)–164, [166](#ch7.xhtml_page_166)

non-interrupt blink LED timer, [149](#ch7.xhtml_page_149)–155

Nucleo-64 board options, [22](#ch1.xhtml_page_22)

polled blink LED timer, [149](#ch7.xhtml_page_149)–155

light-emitting diode. *See* LED

loader, [34](#ch2.xhtml_page_34)

Lock, [170](#ch8.xhtml_page_170)

low-ass analog filter, [260](#ch11.xhtml_page_260)

low clock speed, [127](#ch5.xhtml_page_127)

low power timers, [147](#ch7.xhtml_page_147)

low-speed external clock (LSE), [24](#ch1.xhtml_page_24), [62](#ch3.xhtml_page_62)–63

LR register, [132](#ch6.xhtml_page_132)

LSE. *See* low-speed external clock (LSE)

maskable interrupt, [131](#ch6.xhtml_page_131)

master clock, [145](#ch7.xhtml_page_145)

master clock output (MCO), [23](#ch1.xhtml_page_23)

*Mastering STM32* (Noviello), [53](#ch3.xhtml_page_53)

maximum ambient temperature (TAMAX), [65](#ch3.xhtml_page_65)

MCO. *See* master clock output (MCO)

MCU. *See* microcontroller (MCU)

MCU pinout diagram, [40](#ch2.xhtml_page_40), [40](#ch2.xhtml_page_40)f

MCU toolchain, [32](#ch2.xhtml_page_32)–52

debugging tool. *See* OpenOCD15

integrated development environment (IDE), [32](#ch2.xhtml_page_32)

Keil IDE, [35](#ch2.xhtml_page_35)–36

ST-LINK, [40](#ch2.xhtml_page_40)–43

STMCubeMX, [37](#ch2.xhtml_page_37)–40

toolchain workflow, [33](#ch2.xhtml_page_33)f, [34](#ch2.xhtml_page_34)

`mdb` command, [52](#ch2.xhtml_page_52), [52](#ch2.xhtml_page_52)f

`mdh` command, [52](#ch2.xhtml_page_52), [52](#ch2.xhtml_page_52)f

MDK-ARM subdirectory, [82](#ch3.xhtml_page_82)

MDK-ARM V4, [88](#ch4.xhtml_page_88)

MDK474.exe, [36](#ch2.xhtml_page_36)

`mdw` command, [52](#ch2.xhtml_page_52), [52](#ch2.xhtml_page_52)f

memory, [5](#ch1.xhtml_page_5)–6

memory management unit (MMU), [103](#ch5.xhtml_page_103)

memory-mapped peripherals, [103](#ch5.xhtml_page_103)

memory mapping, [103](#ch5.xhtml_page_103)

memory port, [245](#ch11.xhtml_page_245)

memory protection unit (MPU), [105](#ch5.xhtml_page_105)

memory-to-memory transfer, [244](#ch11.xhtml_page_244)

memory-to-peripheral transfer, [244](#ch11.xhtml_page_244)

microcomputer, [1](#ch1.xhtml_page_1)

microcontroller (MCU)

analog-to-digital converter (ADC), [16](#ch1.xhtml_page_16)

bit serial ports, [19](#ch1.xhtml_page_19)–21

components, [3](#ch1.xhtml_page_3)–21

defined, [1](#ch1.xhtml_page_1)

external interrupt/event controller (EXTI), [16](#ch1.xhtml_page_16)

general purpose input-outputs (GPIOs), [16](#ch1.xhtml_page_16)

historical overview, [30](#ch2.xhtml_page_30)–31

I2C serial protocol, [19](#ch1.xhtml_page_19)–20

inter-integrated sound (I2S) interface, [21](#ch1.xhtml_page_21)

memory, [5](#ch1.xhtml_page_5)–6

microprocessor, compared, [1](#ch1.xhtml_page_1)

nested vector interrupt controller (NVIC), [14](#ch1.xhtml_page_14)–16

peripherals, [6](#ch1.xhtml_page_6)–13

processor, [3](#ch1.xhtml_page_3)–5

SPI serial protocol, [20](#ch1.xhtml_page_20)–21

timers and counters, [16](#ch1.xhtml_page_16)–19

USART serial protocol, [19](#ch1.xhtml_page_19)

microprocessor, [1](#ch1.xhtml_page_1)

MiddleWares, [58](#ch3.xhtml_page_58)

MMU. *See* memory management unit (MMU)

Mode, [172](#ch8.xhtml_page_172)

MODER, [111](#ch5.xhtml_page_111)

modulus operator, [165](#ch7.xhtml_page_165)

Morpho connectors, [13](#ch1.xhtml_page_13), [114](#ch5.xhtml_page_114)f

MPU. *See* memory protection unit (MPU)

multi-channel oscilloscope, [125](#ch5.xhtml_page_125)

multi-channel scan/ continuous conversion, [198](#ch9.xhtml_page_198)

multi-channel scan/single conversion, [197](#ch9.xhtml_page_197)–198, [198](#ch9.xhtml_page_198)f

multi-rate interrupt-driven blink LED timer, [157](#ch7.xhtml_page_157)–164, [166](#ch7.xhtml_page_166)

multiple brace pairs, [97](#ch4.xhtml_page_97)

`MX_GPIO_Init ( )`

CubeMX, [78](#ch3.xhtml_page_78)

interrupt, [138](#ch6.xhtml_page_138), [141](#ch6.xhtml_page_141)

STM project development, [93](#ch4.xhtml_page_93), [97](#ch4.xhtml_page_97)

timers, [155](#ch7.xhtml_page_155)

N-BIT REGISTER, [190](#ch9.xhtml_page_190)–192

nested vector interrupt controller (NVIC), [14](#ch1.xhtml_page_14)–16, [129](#ch6.xhtml_page_129), [130](#ch6.xhtml_page_130)–131

nesting, [97](#ch4.xhtml_page_97)

New C/C++ Project dialog box, [88](#ch4.xhtml_page_88)f

New Project (CubeMX), [55](#ch3.xhtml_page_55), [66](#ch3.xhtml_page_66)–78

Application/MDK-ARM, [70](#ch3.xhtml_page_70)f

Application/User, [70](#ch3.xhtml_page_70)f

Code Generation dialog box, [68](#ch3.xhtml_page_68), [69](#ch3.xhtml_page_69)f

Code Generator screen, [68](#ch3.xhtml_page_68), [69](#ch3.xhtml_page_69)f

Device Database menu selection, [71](#ch3.xhtml_page_71), [71](#ch3.xhtml_page_71)f

Device not found dialog box, [71](#ch3.xhtml_page_71), [71](#ch3.xhtml_page_71)f

Drivers/CMSIS, [70](#ch3.xhtml_page_70)f

Drivers/STM32F3xx_HAL_Driver, [70](#ch3.xhtml_page_70)f

`HAL_Init ( )`, [78](#ch3.xhtml_page_78)

main.c code listing, [72](#ch3.xhtml_page_72)–78

`MX_GPIO_Init ( )`, [78](#ch3.xhtml_page_78)

Open Project button, [68](#ch3.xhtml_page_68)

opening screen, [66](#ch3.xhtml_page_66)f

Project dropdown menu, [66](#ch3.xhtml_page_66), [67](#ch3.xhtml_page_67)f

Project Settings screen, [67](#ch3.xhtml_page_67)–68, [67](#ch3.xhtml_page_67)f

Project Settings submenu, [68](#ch3.xhtml_page_68)

STM disclaimer, [72](#ch3.xhtml_page_72), [73](#ch3.xhtml_page_73)f

STM32F302RB selection, [72](#ch3.xhtml_page_72), [72](#ch3.xhtml_page_72)f

STM32Nucleo_F302 project directories, [68](#ch3.xhtml_page_68), [70](#ch3.xhtml_page_70)f

`SystemClock_Config ( )`, [78](#ch3.xhtml_page_78)

`while (1)` statement, [78](#ch3.xhtml_page_78)

New Project opening screen, [66](#ch3.xhtml_page_66)f

NMI. *See* non-maskable interrupt (NMI)

noise, [260](#ch11.xhtml_page_260)

non-interrupt blink LED timer, [149](#ch7.xhtml_page_149)–155

non-maskable interrupt (NMI), [130](#ch6.xhtml_page_130), [130](#ch6.xhtml_page_130)f

Noviello, Carmine, [53](#ch3.xhtml_page_53)

NRST, [11](#ch1.xhtml_page_11), [58](#ch3.xhtml_page_58)f, [59](#ch3.xhtml_page_59)

Nucleo board user manual, [113](#ch5.xhtml_page_113)

Nucleo boards, [2](#ch1.xhtml_page_2)–3

Nucleo-32 board, [3](#ch1.xhtml_page_3)f

Nucleo-64 block diagram, [7](#ch1.xhtml_page_7)f

Nucleo-64 board, [3](#ch1.xhtml_page_3), [3](#ch1.xhtml_page_3)f

Nucleo-64 board layout, [6](#ch1.xhtml_page_6)–13

Nucleo-64 board options, [22](#ch1.xhtml_page_22)–27

JP6, [23](#ch1.xhtml_page_23)

LEDs, [22](#ch1.xhtml_page_22)

OSC [32](#ch2.xhtml_page_32)-kHz clock supply, [24](#ch1.xhtml_page_24)

OSC clock, [23](#ch1.xhtml_page_23)–24

power supply and power selection, [24](#ch1.xhtml_page_24)–27

push buttons, [22](#ch1.xhtml_page_22)–23

Nucleo-64 NUCLEO-F302R8 board, [39](#ch2.xhtml_page_39), [39](#ch2.xhtml_page_39)f

Nucleo-64 pinout diagram, [10](#ch1.xhtml_page_10)f

Nucleo-144 board, [3](#ch1.xhtml_page_3)f

NUCLEO-F302R8 board, [39](#ch2.xhtml_page_39), [39](#ch2.xhtml_page_39)f

NUCLEO-F302R8 board selection, [55](#ch3.xhtml_page_55), [57](#ch3.xhtml_page_57)f

NUCLEO-F411RE development board, [58](#ch3.xhtml_page_58)

NVIC. *See* nested vector interrupt controller (NVIC)

NVIC BASEPRI register, [131](#ch6.xhtml_page_131)–132

NVIC block diagram, [130](#ch6.xhtml_page_130)f

Open On-Chip Debugger, [43](#ch2.xhtml_page_43). *See also* OpenOCD15

Open Project button, [68](#ch3.xhtml_page_68)

Open-source vs. commercial proprietary software, [29](#ch2.xhtml_page_29)–30

opening and closing braces { }, [96](#ch4.xhtml_page_96), [97](#ch4.xhtml_page_97)

OpenOCD15, [43](#ch2.xhtml_page_43)–52

accessing the program, [44](#ch2.xhtml_page_44)

finish screen, [45](#ch2.xhtml_page_45)f

GNU Project Debugger (GDB), [44](#ch2.xhtml_page_44)–45

gnuarmeclipse-openocd-win64-0.10.0-201701241841-setup.exe, [43](#ch2.xhtml_page_43), [44](#ch2.xhtml_page_44)f

help request, [49](#ch2.xhtml_page_49), [49](#ch2.xhtml_page_49)f

memory content display commands, [51](#ch2.xhtml_page_51)–52, [52](#ch2.xhtml_page_52)f

opening screen, [45](#ch2.xhtml_page_45)f

`reg` command after a halt, [51](#ch2.xhtml_page_51), [51](#ch2.xhtml_page_51)f

`reg` command after a reset, [50](#ch2.xhtml_page_50)f, [51](#ch2.xhtml_page_51)

service or background program, [44](#ch2.xhtml_page_44)

starting OpenOCD service, [47](#ch2.xhtml_page_47)f

Telnet link, [46](#ch2.xhtml_page_46)–48

user guide, [49](#ch2.xhtml_page_49)–50

versions, [43](#ch2.xhtml_page_43), [44](#ch2.xhtml_page_44)f

Zadig utility, [47](#ch2.xhtml_page_47)–48

OpenOCD15 downloads, [44](#ch2.xhtml_page_44)f

OpenOCD15 finish screen, [45](#ch2.xhtml_page_45)f

OpenOCD15 opening screen, [45](#ch2.xhtml_page_45)f

OpenOCD15 user guide, [49](#ch2.xhtml_page_49)–50

OSC [32](#ch2.xhtml_page_32)-kHz clock supply, [24](#ch1.xhtml_page_24)

OSC clock, [23](#ch1.xhtml_page_23)–24

output capture, [17](#ch1.xhtml_page_17), [146](#ch7.xhtml_page_146)

overclocking, [63](#ch3.xhtml_page_63)

overflow interrupt, [145](#ch7.xhtml_page_145)

OverSampling, [172](#ch8.xhtml_page_172)

PA2, [19](#ch1.xhtml_page_19), [58](#ch3.xhtml_page_58)f, [59](#ch3.xhtml_page_59), [174](#ch8.xhtml_page_174)

PA3, [19](#ch1.xhtml_page_19), [58](#ch3.xhtml_page_58)f, [59](#ch3.xhtml_page_59), [174](#ch8.xhtml_page_174)

PA6, [122](#ch5.xhtml_page_122)

PA10, [115](#ch5.xhtml_page_115), [117](#ch5.xhtml_page_117), [122](#ch5.xhtml_page_122)

Parity, [172](#ch8.xhtml_page_172)

PB13, [58](#ch3.xhtml_page_58)f, [59](#ch3.xhtml_page_59)

PC. *See* program counter (PC)

PC13, [58](#ch3.xhtml_page_58)f, [59](#ch3.xhtml_page_59)

PC13 alternative pin mappings, [60](#ch3.xhtml_page_60)f

PC register, [132](#ch6.xhtml_page_132)

PCC. *See* power consumption calculator (PCC)

PDSC, [79](#ch3.xhtml_page_79)

pending interrupt request, [133](#ch6.xhtml_page_133)

peripheral memory addresses, [105](#ch5.xhtml_page_105)–108

peripheral port, [245](#ch11.xhtml_page_245)

peripheral-to-memory transfer, [244](#ch11.xhtml_page_244)

peripheral-to-peripheral transfer, [244](#ch11.xhtml_page_244)

peripherals, [6](#ch1.xhtml_page_6)–13

phase-locked loop (PLL), [145](#ch7.xhtml_page_145)

Picoscope USB oscilloscope, [125](#ch5.xhtml_page_125)

pin clock speeds, [125](#ch5.xhtml_page_125)–126

pinout diagram, [40](#ch2.xhtml_page_40), [40](#ch2.xhtml_page_40)f

Pinout tab, [58](#ch3.xhtml_page_58)–60

PLL. *See* phase-locked loop (PLL)

polled blink LED timer, [149](#ch7.xhtml_page_149)–155

polling

analog-to-digital conversion, [201](#ch9.xhtml_page_201)–212

interrupts, [133](#ch6.xhtml_page_133)–134

Port, [173](#ch8.xhtml_page_173)

Ports (COM & LPT), [173](#ch8.xhtml_page_173), [174](#ch8.xhtml_page_174)

power consumption calculator (PCC), [65](#ch3.xhtml_page_65)f

Power Consumption Calculator View tab, [65](#ch3.xhtml_page_65)

power-on sequence procedure, [27](#ch1.xhtml_page_27)

power supply and power selection, [24](#ch1.xhtml_page_24)–27

preemption and interrupt nesting, [15](#ch1.xhtml_page_15)f

prescaler, [145](#ch7.xhtml_page_145), [147](#ch7.xhtml_page_147)–148

prioritized interrupt, [15](#ch1.xhtml_page_15), [131](#ch6.xhtml_page_131)

priority assignment hardware unit, [245](#ch11.xhtml_page_245)

processor, [3](#ch1.xhtml_page_3)–5

Program and Verify dialog box, [85](#ch3.xhtml_page_85)f

program counter (PC), [14](#ch1.xhtml_page_14)

project build, [100](#ch4.xhtml_page_100). *See also* STM project development

Project dropdown menu, [66](#ch3.xhtml_page_66), [67](#ch3.xhtml_page_67)f, [88](#ch4.xhtml_page_88), [89](#ch4.xhtml_page_89)f

Project pinout screen, [88](#ch4.xhtml_page_88), [89](#ch4.xhtml_page_89)f

Project Settings/Code Generator dialog box, [89](#ch4.xhtml_page_89)–90, [91](#ch4.xhtml_page_91)f

Project Settings dialog box, [88](#ch4.xhtml_page_88)–89, [90](#ch4.xhtml_page_90)f

Project Settings screen, [67](#ch3.xhtml_page_67)–68, [67](#ch3.xhtml_page_67)f

Project Settings submenu, [68](#ch3.xhtml_page_68)

pRxBuffPtr, [170](#ch8.xhtml_page_170)

pTxBuffPtr, [170](#ch8.xhtml_page_170)

pulse-width modulation (PWM), [213](#ch10.xhtml_page_213)–240

50% duty cycle waveform, [227](#ch10.xhtml_page_227)–228, [229](#ch10.xhtml_page_229)t

CIE1931 lightness formula, [231](#ch10.xhtml_page_231)

color and luminescence of tricolor LED, [231](#ch10.xhtml_page_231)–235

duty cycle, [214](#ch10.xhtml_page_214)

enabling PWM function, [220](#ch10.xhtml_page_220)–222

frequency, [213](#ch10.xhtml_page_213)–214

general-purpose timer PWM signal generation, [214](#ch10.xhtml_page_214)–216

HAL framework, [216](#ch10.xhtml_page_216)–220

hobby-grade servo motor, [235](#ch10.xhtml_page_235)–239

human eye brightness perception, [229](#ch10.xhtml_page_229), [230](#ch10.xhtml_page_230)f

luminescence of normal LED, [228](#ch10.xhtml_page_228)–231

purposes, [213](#ch10.xhtml_page_213)

PWM demonstration software, [222](#ch10.xhtml_page_222)–227

timer hardware architecture, [216](#ch10.xhtml_page_216), [217](#ch10.xhtml_page_217)f

typical PWM signal, [214](#ch10.xhtml_page_214)f

push button test demonstration, [123](#ch5.xhtml_page_123)–124, [128](#ch5.xhtml_page_128)

push buttons, [22](#ch1.xhtml_page_22)–23

push pins, [61](#ch3.xhtml_page_61)

PWM. *See* pulse-width modulation (PWM)

R-2R resistor ladder network, [259](#ch11.xhtml_page_259), [259](#ch11.xhtml_page_259)f

rank, [199](#ch9.xhtml_page_199), [199](#ch9.xhtml_page_199)f

Rath, Dominic, [43](#ch2.xhtml_page_43)

`raw = (double) HAL_ADC_GetValue (&hadc1)`, [206](#ch9.xhtml_page_206)

`raw = raw * 0.452`, [206](#ch9.xhtml_page_206)

RCC global interrupt, [142](#ch6.xhtml_page_142)–143

RCC pin configurations, [63](#ch3.xhtml_page_63)

real-time operating system (RTOS), [18](#ch1.xhtml_page_18), [79](#ch3.xhtml_page_79), [105](#ch5.xhtml_page_105)

Realterm Port screen, [173](#ch8.xhtml_page_173)f

Realterm terminal program, [172](#ch8.xhtml_page_172)–175

reference manual, [101](#ch5.xhtml_page_101)

`reg` command, [50](#ch2.xhtml_page_50)f, [51](#ch2.xhtml_page_51), [51](#ch2.xhtml_page_51)f

Reinstall WinUSB driver dialog box, [48](#ch2.xhtml_page_48)f

RepetitionCounter, [148](#ch7.xhtml_page_148)

request/acknowledge, [169](#ch8.xhtml_page_169)

request-to-send (RTS) line, [169](#ch8.xhtml_page_169)

`reset` command, [50](#ch2.xhtml_page_50)f, [51](#ch2.xhtml_page_51)

Round Robin algorithm, [244](#ch11.xhtml_page_244)

RTOS. *See* real-time operating system (RTOS)

RTS. *See* request-to-send (RTS) line

RxXferCount, [170](#ch8.xhtml_page_170)

sample/hold circuit, [190](#ch9.xhtml_page_190)

SAR. *See* successive-approximation register (SAR)

SAR LOGIC module, [191](#ch9.xhtml_page_191), [191](#ch9.xhtml_page_191)f

SB13, [19](#ch1.xhtml_page_19)

SB14, [19](#ch1.xhtml_page_19)

SB62, [19](#ch1.xhtml_page_19), [175](#ch8.xhtml_page_175)

SB63, [19](#ch1.xhtml_page_19), [175](#ch8.xhtml_page_175)

serial peripheral interface. *See* SPI

servo motor, [235](#ch10.xhtml_page_235)–239

signal waveforms, [126](#ch5.xhtml_page_126), [126](#ch5.xhtml_page_126)f

simple [16](#ch1.xhtml_page_16)-bit timer, [17](#ch1.xhtml_page_17)t, [18](#ch1.xhtml_page_18), [146](#ch7.xhtml_page_146), [147](#ch7.xhtml_page_147)t

simpler code vs. compact, complex code, [165](#ch7.xhtml_page_165)

sine wave signals, [269](#ch11.xhtml_page_269)–278

single channel/continuous conversion, [198](#ch9.xhtml_page_198)

single channel/single conversion, [197](#ch9.xhtml_page_197), [197](#ch9.xhtml_page_197)f

slave port, [245](#ch11.xhtml_page_245)

software. *See* STM MCU software

source code, [34](#ch2.xhtml_page_34)

SPI, [20](#ch1.xhtml_page_20)–21

SPI block diagram, [21](#ch1.xhtml_page_21)f

SPI2 signal lines, [21](#ch1.xhtml_page_21)t

`sprintf (msg, “%frn,” value)`, [180](#ch8.xhtml_page_180), [206](#ch9.xhtml_page_206), [207](#ch9.xhtml_page_207)

SRAM, [105](#ch5.xhtml_page_105)t

SSI. *See* synchronous serial interface (SSI)

ST-LINK, [40](#ch2.xhtml_page_40)–43, [82](#ch3.xhtml_page_82)–86

ST-LINK firmware version display, [43](#ch2.xhtml_page_43)f

ST-LINK/V2 opening screen, [41](#ch2.xhtml_page_41)f

`static void MX_ADC1_Init (void)`, [204](#ch9.xhtml_page_204)

`static void MX_TIM2_Init (void)`, [220](#ch10.xhtml_page_220), [221](#ch10.xhtml_page_221)

`static void MX_USART2_UART_Init (void)`, [175](#ch8.xhtml_page_175), [176](#ch8.xhtml_page_176)

stlink_winusb_install, [41](#ch2.xhtml_page_41)

STM. *See* STMicroelectronics (STM)

STM core memory address ranges, [105](#ch5.xhtml_page_105)t

STM disclaimer, [72](#ch3.xhtml_page_72), [73](#ch3.xhtml_page_73)f

STM GPIO port pin block diagram/schematic, [109](#ch5.xhtml_page_109)f

STM MCU databases, [2](#ch1.xhtml_page_2)

STM MCU interrupt, [144](#ch6.xhtml_page_144). *See also* interrupt

STM MCU software, [29](#ch2.xhtml_page_29)–52

bare metal development, [30](#ch2.xhtml_page_30)

open-source vs. commercial proprietary software, [29](#ch2.xhtml_page_29)–30

toolchain. *See* MCU toolchain

STM Nucleo board user manual, [113](#ch5.xhtml_page_113)

STM Nucleo boards, [2](#ch1.xhtml_page_2)–3

STM Nucleo-64 microcontroller, [27](#ch1.xhtml_page_27). *See also* microcontroller (MCU)

STM project development, [87](#ch4.xhtml_page_87)–100

complex modification of main.c file, [99](#ch4.xhtml_page_99)–100

error dialog, [90](#ch4.xhtml_page_90)–91, [92](#ch4.xhtml_page_92)f

explanation of C/C++ code, [96](#ch4.xhtml_page_96)–97

Keil IDE, [90](#ch4.xhtml_page_90), [92](#ch4.xhtml_page_92)f

main.c file, [91](#ch4.xhtml_page_91)–97

MDK-ARM V4, [88](#ch4.xhtml_page_88)

New C/C++ Project dialog box, [88](#ch4.xhtml_page_88)f

Project dropdown menu, [88](#ch4.xhtml_page_88), [89](#ch4.xhtml_page_89)f

Project pinout screen, [88](#ch4.xhtml_page_88), [89](#ch4.xhtml_page_89)f

Project Settings/Code Generator dialog box, [89](#ch4.xhtml_page_89)–90, [91](#ch4.xhtml_page_91)f

Project Settings dialog box, [88](#ch4.xhtml_page_88)–89, [90](#ch4.xhtml_page_90)f

simple modification of main.c file, [98](#ch4.xhtml_page_98)–99

Successful Code Generation dialog box, [90](#ch4.xhtml_page_90), [91](#ch4.xhtml_page_91)f

STM timer peripherals, [145](#ch7.xhtml_page_145)–147\. *See also* timers

STM32-ST-LINK Utility V4.0.0 setup application, [41](#ch2.xhtml_page_41)

STM32 toolchain, [33](#ch2.xhtml_page_33). *See also* MCU toolchain

STM32CubeMX, [37](#ch2.xhtml_page_37)–40, [53](#ch3.xhtml_page_53)–86\. *See also* CubeMX

STM32CubeMX opening splash screen, [37](#ch2.xhtml_page_37)f, [54](#ch3.xhtml_page_54)f

STM32F302R8 block diagram, [101](#ch5.xhtml_page_101), [102](#ch5.xhtml_page_102)f

STM32F302R8 datasheet, [101](#ch5.xhtml_page_101)

STM32F302R8 MCU, [6](#ch1.xhtml_page_6), [27](#ch1.xhtml_page_27), [32](#ch2.xhtml_page_32)t

STM32F302R8 MCU pinout diagram, [40](#ch2.xhtml_page_40), [40](#ch2.xhtml_page_40)f

STM32F302R8 reference manual, [101](#ch5.xhtml_page_101)

STM32F302RB selection, [72](#ch3.xhtml_page_72), [72](#ch3.xhtml_page_72)f

STM32F302R8Tx MCU, [58](#ch3.xhtml_page_58)f

stm32f3xx_it.c file listing, [142](#ch6.xhtml_page_142)

STMicroelectronics (STM), [29](#ch2.xhtml_page_29)

STM32Nucleo_F302 project directories, [68](#ch3.xhtml_page_68), [70](#ch3.xhtml_page_70)f

STM32Toolchain directory, [37](#ch2.xhtml_page_37)

st_nucleo_f3.cfg, [46](#ch2.xhtml_page_46), [46](#ch2.xhtml_page_46)t

StopBits, [171](#ch8.xhtml_page_171)

STSW-LINK004, [41](#ch2.xhtml_page_41)

STSW-LINK009, [40](#ch2.xhtml_page_40)

Successful Code Generation dialog box, [90](#ch4.xhtml_page_90), [91](#ch4.xhtml_page_91)f

successive-approximation register (SAR), [190](#ch9.xhtml_page_190), [191](#ch9.xhtml_page_191)f

SVD. *See* System View Description (SVD)

synchronous serial data link, [20](#ch1.xhtml_page_20)

synchronous serial interface (SSI), [20](#ch1.xhtml_page_20)

synthesizing a sine wave, [270](#ch11.xhtml_page_270)

system memory, [105](#ch5.xhtml_page_105)t

System View Description (SVD), [79](#ch3.xhtml_page_79)

`SystemClock_Config ( )`, [78](#ch3.xhtml_page_78), [93](#ch4.xhtml_page_93), [97](#ch4.xhtml_page_97)

SysTick interrupt, [131](#ch6.xhtml_page_131), [133](#ch6.xhtml_page_133)

SysTick timer, [18](#ch1.xhtml_page_18)–19

tail-chaining, [15](#ch1.xhtml_page_15)f

TAMAX. *See* maximum ambient temperature (TAMAX)

Telnet link, [46](#ch2.xhtml_page_46)–48

Telnet scripts, [46](#ch2.xhtml_page_46)t

terminal program, [172](#ch8.xhtml_page_172)–175

THD. *See* total harmonic distortion (THD)

TIM1\. *See* advanced control timer (TIM1)

TIM2, [17](#ch1.xhtml_page_17), [17](#ch1.xhtml_page_17)t, [147](#ch7.xhtml_page_147)t

TIM2 clock source selection, [149](#ch7.xhtml_page_149)f

TIM6, [17](#ch1.xhtml_page_17)t, [18](#ch1.xhtml_page_18), [147](#ch7.xhtml_page_147)t

TIM15, [17](#ch1.xhtml_page_17), [17](#ch1.xhtml_page_17)t, [147](#ch7.xhtml_page_147)t

TIM16, [17](#ch1.xhtml_page_17), [17](#ch1.xhtml_page_17)t, [147](#ch7.xhtml_page_147)t

TIM17, [17](#ch1.xhtml_page_17), [17](#ch1.xhtml_page_17)t, [147](#ch7.xhtml_page_147)t

TIM_CLOCKDIVISION_DIV, [148](#ch7.xhtml_page_148)

TIM_CLOCKDIVISION_DIV2, [148](#ch7.xhtml_page_148)

TIM_CLOCKDIVISION_DIV4, [148](#ch7.xhtml_page_148)

TIM_COUNTERMODE_CENTERALIGNED1, [148](#ch7.xhtml_page_148)

TIM_COUNTERMODE_CENTERALIGNED2, [148](#ch7.xhtml_page_148)

TIM_COUNTERMODE_CENTERALIGNED3, [148](#ch7.xhtml_page_148)

TIM_COUNTERMODE_DOWN, [148](#ch7.xhtml_page_148)

TIM_COUNTERMODE_UP, [148](#ch7.xhtml_page_148)

timer counter (CNT), [216](#ch10.xhtml_page_216), [217](#ch10.xhtml_page_217)f

timer hardware architecture, [216](#ch10.xhtml_page_216), [217](#ch10.xhtml_page_217)f

timer update register, [148](#ch7.xhtml_page_148)

timers, [16](#ch1.xhtml_page_16)–19, [145](#ch7.xhtml_page_145)–166

categories, [146](#ch7.xhtml_page_146)–147

configuration, [147](#ch7.xhtml_page_147)–149

counting up/counting down, [145](#ch7.xhtml_page_145)

decrementing counter, [145](#ch7.xhtml_page_145)

definition, [145](#ch7.xhtml_page_145)

hardware architecture, [216](#ch10.xhtml_page_216), [217](#ch10.xhtml_page_217)f

interrupt-driven blink LED timer, [155](#ch7.xhtml_page_155)–157

manufacturer datasheets, [147](#ch7.xhtml_page_147)

master clock, [145](#ch7.xhtml_page_145)

multi-rate interrupt-driven blink LED timer, [157](#ch7.xhtml_page_157)–164, [166](#ch7.xhtml_page_166)

non-interrupt blink LED timer, [149](#ch7.xhtml_page_149)–155

overflow interrupt, [145](#ch7.xhtml_page_145)

parameters and settings, [147](#ch7.xhtml_page_147)–148

polled blink LED timer, [149](#ch7.xhtml_page_149)–155

STM32F302R8 MCU timers, [17](#ch1.xhtml_page_17)t, [147](#ch7.xhtml_page_147)t

timer update register, [148](#ch7.xhtml_page_148)

trade-off (simpler code vs. compact, complex code), [165](#ch7.xhtml_page_165)

update event calculation, [148](#ch7.xhtml_page_148)–149

uses, [146](#ch7.xhtml_page_146)

`TIM_HandleTypeDef`, [147](#ch7.xhtml_page_147), [155](#ch7.xhtml_page_155)

`TIM_MasterConfigTypeDef`, [216](#ch10.xhtml_page_216)

TIM_MASTERSLAVEMODE_DISABLE, [216](#ch10.xhtml_page_216)

TIM_MASTERSLAVEMODE_ENABLE, [216](#ch10.xhtml_page_216)

TIM_OCIDLESTATE_RESET, [219](#ch10.xhtml_page_219)

TIM_OCIDLESTATE_SET, [219](#ch10.xhtml_page_219)

`TIM_OC_InitTypeDef`, [218](#ch10.xhtml_page_218)

TIM_OCMODE_ACTIVE, [218](#ch10.xhtml_page_218)

TIM_OCMODE_FORCED_ACTIVE, [218](#ch10.xhtml_page_218)

TIM_OCMODE_FORCED_INACTIVE, [218](#ch10.xhtml_page_218)

TIM_OCMODE_INACTIVE, [218](#ch10.xhtml_page_218)

TIM_OCMODE_PWM1-PWM Mode [1](#ch1.xhtml_page_1), [218](#ch10.xhtml_page_218)

TIM_OCMODE_PWM2-PWM Mode [2](#ch1.xhtml_page_2), [218](#ch10.xhtml_page_218)

TIM_OCMODE_TIMING, [218](#ch10.xhtml_page_218)

TIM_OCMODE_TOGGLE, [218](#ch10.xhtml_page_218)

TIM_OCNFAST_DISABLE, [219](#ch10.xhtml_page_219)

TIM_OCNFAST_ENABLE, [219](#ch10.xhtml_page_219)

TIM_OCNIDLESTATE_RESET, [220](#ch10.xhtml_page_220)

TIM_OCNIDLESTATE_SET, [220](#ch10.xhtml_page_220)

TIM_OCNPOLARITY_HIGH, [219](#ch10.xhtml_page_219)

TIM_OCNPOLARITY_LOW, [219](#ch10.xhtml_page_219)

TIM_OCPOLARITY_HIGH, [219](#ch10.xhtml_page_219)

TIM_OCPOLARITY_LOW, [219](#ch10.xhtml_page_219)

TMP36 temperature sensor, [189](#ch9.xhtml_page_189), [190](#ch9.xhtml_page_190)f, [202](#ch9.xhtml_page_202)–205

TMS1000, [30](#ch2.xhtml_page_30)

toggle method, [165](#ch7.xhtml_page_165)

toolchain, [32](#ch2.xhtml_page_32). *See also* MCU toolchain

toolchain workflow, [33](#ch2.xhtml_page_33)f, [34](#ch2.xhtml_page_34)

total harmonic distortion (THD), [277](#ch11.xhtml_page_277)

track/hold circuit, [190](#ch9.xhtml_page_190)

trade-off (simpler code vs. compact, complex code), [165](#ch7.xhtml_page_165)

trailing edge delay, [124](#ch5.xhtml_page_124)

tree pane IP icons, [61](#ch3.xhtml_page_61)f

triangular waveform, [263](#ch11.xhtml_page_263)–269

trivial bug, [34](#ch2.xhtml_page_34)

TxXferCount, [170](#ch8.xhtml_page_170)

UART, [167](#ch8.xhtml_page_167)

UART block diagram, [167](#ch8.xhtml_page_167)f

UART vs. USART, [167](#ch8.xhtml_page_167), [168](#ch8.xhtml_page_168)

`UART_HandleTypeDef`, [170](#ch8.xhtml_page_170)

UART_HWCONTROL_CTS, [172](#ch8.xhtml_page_172)

UART_HWCONTROL_NONE, [172](#ch8.xhtml_page_172)

UART_HWCONTROL_RTS, [172](#ch8.xhtml_page_172)

UART_HWCONTROL_RTS_CTS, [172](#ch8.xhtml_page_172)

`UART_InitTypeDef`, [170](#ch8.xhtml_page_170), [171](#ch8.xhtml_page_171)

UART_MODE_RX, [172](#ch8.xhtml_page_172)

UART_MODE_TX, [172](#ch8.xhtml_page_172)

UART_MODE_TX_RX, [172](#ch8.xhtml_page_172)

UART_OVERSAMPLING_8, [172](#ch8.xhtml_page_172)

UART_OVERSAMPLING_16, [172](#ch8.xhtml_page_172)

UART_PARITY_EVEN, [172](#ch8.xhtml_page_172)

UART_PARITY_NONE, [172](#ch8.xhtml_page_172)

UART_PARITY_ODD, [172](#ch8.xhtml_page_172)

UART_STOPBITS_1, [171](#ch8.xhtml_page_171)

UART_STOPBITS_2, [171](#ch8.xhtml_page_171)

UART_WORDLENGTH-8B, [171](#ch8.xhtml_page_171)

UART_WORDLENGTH-9B, [171](#ch8.xhtml_page_171)

`uint32_t Channel`, [199](#ch9.xhtml_page_199)

`uint32_t ClockPrescaler`, [193](#ch9.xhtml_page_193), [194](#ch9.xhtml_page_194)

`uint32_t ContinuousConvMode`, [193](#ch9.xhtml_page_193), [195](#ch9.xhtml_page_195)

`uint32_t DAC_OutputBuffer`, [262](#ch11.xhtml_page_262)

`uint32_t DAC_Trigger`, [262](#ch11.xhtml_page_262)

`uint32_t DataAlign`, [193](#ch9.xhtml_page_193), [194](#ch9.xhtml_page_194)

`uint32_t Direction`, [249](#ch11.xhtml_page_249)

`uint32_t DiscontinuousConvMode`, [193](#ch9.xhtml_page_193), [195](#ch9.xhtml_page_195)

`uint32_t DMAContinuousRequests`, [194](#ch9.xhtml_page_194), [196](#ch9.xhtml_page_196)

`uint32_t EOCSelection`, [193](#ch9.xhtml_page_193), [195](#ch9.xhtml_page_195)

`uint32_t ExternalTrigConv`, [194](#ch9.xhtml_page_194), [195](#ch9.xhtml_page_195)–196

`uint32_t ExternalTrigConvEdge`, [194](#ch9.xhtml_page_194), [196](#ch9.xhtml_page_196)

`uint32_t HAL_ADC_GetValue (ADC_HandleTypeDef* hadc)`, [201](#ch9.xhtml_page_201)

`uint32_t MasterOutputTrigger`, [216](#ch10.xhtml_page_216)

`uint32_t MasterSlaveMode`, [216](#ch10.xhtml_page_216)

`uint32_t MemDataAlignment`, [249](#ch11.xhtml_page_249)

`uint32_t MemInc`, [249](#ch11.xhtml_page_249)

`uint32_t Mode`, [249](#ch11.xhtml_page_249), [250](#ch11.xhtml_page_250)

`uint32_t NbrOfConversion`, [193](#ch9.xhtml_page_193), [195](#ch9.xhtml_page_195)

`uint32_t OCFastMode`, [218](#ch10.xhtml_page_218), [219](#ch10.xhtml_page_219)

`uint32_t OCIdleState`, [218](#ch10.xhtml_page_218), [219](#ch10.xhtml_page_219)

`uint32_t OCMode`, [218](#ch10.xhtml_page_218)

`uint32_t OCNIdleState`, [218](#ch10.xhtml_page_218), [220](#ch10.xhtml_page_220)

`uint32_t OCNPolarity`, [218](#ch10.xhtml_page_218), [219](#ch10.xhtml_page_219)

`uint32_t OCPolarity,` [`218`](#ch10.xhtml_page_218)`,` [`219`](#ch10.xhtml_page_219)

`uint32_t Offset`, [199](#ch9.xhtml_page_199), [200](#ch9.xhtml_page_200)

`uint32_t PeriphDataAlignment`, [249](#ch11.xhtml_page_249)

`uint32_t PeriphInc`, [249](#ch11.xhtml_page_249)

`uint32_t Priority,` 249, [250](#ch11.xhtml_page_250)

`uint32_t Pulse,` [218](#ch10.xhtml_page_218), [219](#ch10.xhtml_page_219)

`uint32_t Rank`, [199](#ch9.xhtml_page_199)–200

`uint32_t Resolution`, [193](#ch9.xhtml_page_193), [194](#ch9.xhtml_page_194)

`uint32_t SamplingTime`, [199](#ch9.xhtml_page_199), [200](#ch9.xhtml_page_200)

`uint32_t ScanConvMode`, [193](#ch9.xhtml_page_193), [194](#ch9.xhtml_page_194)

`uint32_t* Alignment`, [269](#ch11.xhtml_page_269), [270](#ch11.xhtml_page_270)

`uint32_t* Length`, [269](#ch11.xhtml_page_269), [270](#ch11.xhtml_page_270)

`uint32_t* pData`, [269](#ch11.xhtml_page_269), [270](#ch11.xhtml_page_270)

universal synchronous/asynchronous receiver/transmitter. *See* USART

universal synchronous receiver transmitter. *See* UART

update event calculation, [148](#ch7.xhtml_page_148)–149

USART, [19](#ch1.xhtml_page_19), [167](#ch8.xhtml_page_167), [168](#ch8.xhtml_page_168), [168](#ch8.xhtml_page_168)f

USART block diagram, [168](#ch8.xhtml_page_168)f

USART configuration, [170](#ch8.xhtml_page_170)–172

USART receive demonstration program, [182](#ch8.xhtml_page_182)–188

USART_RX, [174](#ch8.xhtml_page_174), [174](#ch8.xhtml_page_174)f

USART transmit demonstration program, [176](#ch8.xhtml_page_176)–181

USART_TX, [174](#ch8.xhtml_page_174), [174](#ch8.xhtml_page_174)f

USART1, [169](#ch8.xhtml_page_169)

USART2, [19](#ch1.xhtml_page_19), [169](#ch8.xhtml_page_169)

USART2 global interrupt, [182](#ch8.xhtml_page_182)

USART2 sending character string to memory, [251](#ch11.xhtml_page_251)–258

USART3, [19](#ch1.xhtml_page_19)

USB cable, [42](#ch2.xhtml_page_42), [42](#ch2.xhtml_page_42)f

USB oscilloscope, [125](#ch5.xhtml_page_125), [227](#ch10.xhtml_page_227)

USB ST-LINK driver software, [40](#ch2.xhtml_page_40)

U5V, [13](#ch1.xhtml_page_13)

UV EPROM, [31](#ch2.xhtml_page_31)

uVision, [36](#ch2.xhtml_page_36)

`value = (raw - 500.0)/10`, [206](#ch9.xhtml_page_206)

`value = (9*value) /5 +` [`32`](#ch2.xhtml_page_32), [206](#ch9.xhtml_page_206)

VBAT input, [13](#ch1.xhtml_page_13)

vector interrupt list, [15](#ch1.xhtml_page_15)

very fast clock speed, [127](#ch5.xhtml_page_127)

VIN, [11](#ch1.xhtml_page_11)

VIN external power supply, [25](#ch1.xhtml_page_25), [25](#ch1.xhtml_page_25)t, [26](#ch1.xhtml_page_26)

`void *Parent`, [246](#ch11.xhtml_page_246), [248](#ch11.xhtml_page_248)

`void (* XfercpltCallback) (struct _DMA_HandleTypeDef *hdma)`, [246](#ch11.xhtml_page_246), [248](#ch11.xhtml_page_248)

`void (* XferErrorCallback) (struct _DMA_HandleTypeDef *hdma)`, [246](#ch11.xhtml_page_246), [248](#ch11.xhtml_page_248)

`void EXTI15_10_IRQHandler (void)`, [141](#ch6.xhtml_page_141)–142

von Neumann architecture, [5](#ch1.xhtml_page_5)

watchdog timers, [18](#ch1.xhtml_page_18)

`while (1)` statement, [78](#ch3.xhtml_page_78), [93](#ch4.xhtml_page_93), [97](#ch4.xhtml_page_97), [98](#ch4.xhtml_page_98)

Windows terminal program, [172](#ch8.xhtml_page_172)–175

Wordlength, [171](#ch8.xhtml_page_171)

Zadig utility, [47](#ch2.xhtml_page_47)–48