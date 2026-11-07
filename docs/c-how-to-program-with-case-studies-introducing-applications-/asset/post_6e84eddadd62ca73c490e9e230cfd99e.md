
Academic publications, both print and digital. She challenges us at every step of the process to “get it right” and make the best books. Carole Snyder managed the book’s production and interacted with Pearson’s permissions team, promptly clearing our graphics and citations to keep the book on schedule. Erin Sullivan recruited and managed the book’s review team. We selected the cover art, and Chuti Prasertsith designed the cover, adding his special touch of graphics magic.

We wish to acknowledge the efforts of our academic and professional reviewers. Adhering to a tight schedule, the reviewers scrutinized the manuscript, providing countless suggestions for improving the presentation’s accuracy, completeness and timeliness. They helped us make a better book.

| Reviewers | |
|---|---|
| **C How to Program, 9/e Reviewers**<br>Dr. Danny Kalev (Ben-Gurion University of the Negev, A Certified System Analyst, C Expert and Former Member of the C++ Standards Committee)<br>José Antonio González Seco (Parliament of Andalusia) | Ed James Beckham (Altera)<br>John Benito (Blue Pilot Consulting, Inc. and Convener of ISO WG14—the Working Group responsible for the C Programming Language Standard)<br>Dr. John F. Doyle (Indiana University Southeast)<br>Alireza Fazelpour (Palm Beach Community College)<br>Mahesh Hariharan (Microsoft)<br>Hemanth H.M. (Software Engineer at SonicWALL)<br>Kevin Mark Jones (Hewlett Packard)<br>Lawrence Jones (UGS Corp.)<br>Don Kostuch (Independent Consultant)<br>Vytautas Leonavicius (Microsoft)<br>Xiaolong Li (Indiana State University)<br>William Mike Miller (Edison Design Group, Inc.)<br>Tom Rechard (The University of Texas at Arlington)<br>Robert Seacord (Secure Coding Manager at SEI/CERT, author of The CERT C Secure Coding Standard and technical expert for the international standardization working group for the programming language C)<br>Benjamin Seyfarth (University of Southern Mississippi)<br>Gary Sibbits (St. Louis Community College at Meramec)<br>William Smith (Tulsa Community College)<br>Douglas Walls (Senior Staff Engineer, C compiler, Sun Microsystems—now Oracle). |
| **C How to Program, 8/e Reviewers**<br>Dr. Brandon Invergo (GNU/European Bioinformatics Institute)<br>Jim Hogg (Program Manager, C/C++ Compiler Team, Microsoft Corporation)<br>José Antonio González Seco (Parliament of Andalusia)<br>Alan Bunning (Purdue University)<br>Paul Clingan (Ohio State University)<br>Michael Geiger (University of Massachusetts, Lowell)<br>Dr. Danny Kalev (Ben-Gurion University of the Negev, A Certified System Analyst, C Expert and Former Member of the C++ Standards Committee)<br>Jeonghwa Lee (Shippensburg University)<br>Susan Mengel (Texas Tech University)<br>Judith O’Rourke (SUNY at Albany)<br>Chen-Chi Shin (Radford University) | |
| **Other Recent Editions Reviewers (and their affiliations at the time)**<br>William Albrecht (University of South Florida)<br>Ian Barland (Radford University) | |

A special thanks to Prof. Alison Clear, an Associate Professor in the School of Computing at Eastern Institute of Technology (EIT) in New Zealand and co-chair of the **Computing Curricula 2020 (CC2020)** Task Force, which recently released new computing curricula recommendations:

## About the Authors

With more than 100 translations published in Japanese, German, Russian, Spanish, French, Polish, Italian, Simplified Chinese, Traditional Chinese, Korean, Portuguese, Greek, Urdu and Turkish. Dr. Deitel has delivered hundreds of programming courses to academic, corporate, government and military clients.

## About Deitel® & Associates, Inc.

Deitel & Associates, Inc., founded by Paul Deitel and Harvey Deitel, is an internationally recognized authoring and corporate-training organization, specializing in computer programming languages, object technology, mobile app development and Internet and web software technology. The company’s training clients include some of the world’s largest companies, government agencies, branches of the military, and academic institutions. The company offers instructor-led training courses delivered virtually and live at client sites worldwide, and for Pearson Education on O’Reilly Online Learning.

Through its 45-year publishing partnership with Pearson/Prentice Hall, Deitel & Associates, Inc., publishes leading-edge programming textbooks and professional books in print and e-book formats, LiveLessons video courses, O’Reilly Online Learning live webinars and Revel™ interactive multimedia college courses.

To contact Deitel & Associates, Inc. and the authors, or to request a proposal for virtual or on-site, instructor-led training worldwide, write to

deitel@deitel.com

To learn more about Deitel on-site corporate training, visit

https://deitel.com/training

Individuals wishing to purchase Deitel books can do so at

https://amazon.com

Bulk orders by corporations, the government, the military and academic institutions should be placed directly with Pearson. For corporate and government sales, send an email to

corpsales@pearsoned.com

For textbook orders visit

https://pearson.com

Deitel e-books are available in various formats from

- https://www.amazon.com/
- https://www.vitalsource.com/
- https://www.bn.com/
- https://www.redshelf.com/
- https://www.informit.com/
- https://www.chegg.com/

To register for a free 10-day trial to O’Reilly Online Learning, visit

https://deitel.com/LearnWithDeitel

which will forward you to our O’Reilly Online Learning landing page. On that page, click the **Begin a free trial** link.

## Before You Begin

Before using this book, please read this section to understand our conventions and ensure that your computer can compile and run our example programs.

### Font and Naming Conventions

We use fonts to distinguish application elements and C++ code elements from regular text. For on-screen application elements, we use a sans-serif bold font, as in the **File** menu. For C code elements, we use a sans-serif font, as in `sqrt(9)`.

### Obtaining the Code Examples

We maintain the code examples for *C How to Program, 9/e* in a GitHub repository. The book’s web page

https://deitel.com/c-how-to-program-9-e

includes a link to the repository and a link to a ZIP file containing the code. If you download the ZIP file, be sure to extract its contents once the download completes. In our instructions, we assume the examples reside in your user account’s Documents folder in a subfolder named examples.

If you’re not familiar with Git and GitHub but are interested in learning about these essential developer tools, check out their guides at

https://guides.github.com/activities/hello-world/

### Compilers We Use in *C How to Program, 9/e*

We tested *C How to Program, 9/e*’s examples using the following free compilers:

- For Microsoft Windows, we used Microsoft Visual Studio Community edition¹, which includes the Visual C++ compiler and other Microsoft development tools. Visual C++ can compile C code.
- For macOS, we used Apple Xcode, which includes the Clang C compiler. Command-line Clang also can be installed on Linux and Windows systems.
- For Linux, we used the GNU gcc compiler—part of the GNU Compiler Collection (GCC). GNU gcc is already installed on most Linux systems and can be installed on macOS and Windows systems.

¹ At the time of this writing, the current version was Visual Studio 2019 Community edition.

This Before You Begin section describes installing the compilers. Section 1.10’s test-drives demonstrate how to compile and run C programs using these compilers.

### Before You Begin Videos

To help you get started with each of our preferred compilers, we provide Before You Begin videos at:

`https://deitel.com/c-how-to-program-9-e`

We also provide a Before You Begin video demonstrating how to install the GNU GCC Docker container. This enables you to use the gcc compiler on any Docker-enabled computer.² See the section, “Docker and the GNU Compiler Collection (GCC) Docker Container” later in this Before You Begin section.

### Installing Visual Studio Community Edition on Windows

If you use Windows, first ensure that your system meets the requirements for Microsoft Visual Studio Community edition at:

`https://docs.microsoft.com/en-us/visualstudio/releases/2019/system-requirements`

Next, go to:

`https://visualstudio.microsoft.com/downloads/`

Then perform the following installation steps:

1. Click **Free download** under **Community**.
2. Depending on your web browser, you may see a pop-up at the bottom of your screen in which you can click **Run** to start the installation process. If not, double-click the installer file in your **Downloads** folder.
3. In the **User Account Control** dialog, click **Yes** to allow the installer to make changes to your system.
4. In the **Visual Studio Installer** dialog, click **Continue** to allow the installer to download the components it needs for you to configure your installation.
5. For this book’s examples, select the option **Desktop Development with C++**, which includes the Visual C++ compiler and the C and C++ standard libraries.
6. Click **Install**. Depending on your Internet connection speed, the installation process can take a significant amount of time.

### Installing Xcode on macOS

On macOS, perform the following steps to install Xcode:

1. Click the Apple menu and select **App Store...**, or click the **App Store** icon in the dock at the bottom of your Mac screen.
