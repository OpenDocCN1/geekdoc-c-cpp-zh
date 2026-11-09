
## A Reader for Programmers

faster. Features such as lead-in and lead-out, multiple contouring passes, segmentation of depth cuts, and stock allowances all contribute to a software that becomes easier and more efficient to use. Their inclusion requires another important skill — understanding the actual purpose of all these features. You must understand when to use them and how to use them correctly. You must also have a solid knowledge of machining techniques.

There are many times when even the best features of CAM software may not provide the desired result. Often it is necessary to add a bit of geometry here and there, a little extra tweak to get the exact result required. The part programmer should have an exact vision of the tool path in mind — before even starting to use the computer.

With all this in mind, what is a reasonable learning curve for using CAM software? Is the computer guru in the shop, who has minimal if any knowledge of machining, better suited for the task than the experienced machinist with limited computer knowledge? Most people will agree that learning how to operate and use a computer and software may take a few weeks at the most, whereas learning the art of machining takes years, even a lifetime.

The learning curve for any individual will also depend on other personal and professional skills. Even in CAM programming, there is always some math involved. There is also the entire area of understanding productivity, efficiency, and safety issues in manufacturing. On the technical side, knowledge of the machine tool, the control system, the fixturing, tooling, setup methods, speeds and feeds, and so on, is most important for each and every program developed. In a nutshell, the same qualities and skills required from a part programmer using manual methods are required from a CAM programmer. Unfortunately, this is not always the case.

So who is this CAM machinist from the headline? I believe that the inescapable truth is that you have to know *how to machine a part* before you can be a successful CAM programmer.

Consider the realities. Your customer faxes you a drawing, asking for a quote. Your quote wins and you get the work. Often that faxed drawing is the only drawing you have from which to make the part. In a better scenario, the customer sends you a clean paper drawing. Or better yet, the customer sends you the drawing in the form of a disk file. Now, that is the best scenario, but — yes there are “buts” here.

As most work in the job shops is two dimensional (2D), the design is often done in CAD software such as AutoCAD by the customer. Shops that have CAM capabilities use a tool path development software such as Mastercam, EdgeCam, or GibbsCam. The question is how to get the drawing file into the CAM software. The ideal method is that the software reads the file in its native format. For example, the popular Mastercam can read and write AutoCAD DWG files directly, without a translator. If the software cannot read the native format of the original, it has to have a reliable translator.

Virtually all systems support DXF (drawing exchange file) and/or IGES (Initial Graphics Exchange Specification). DXF is quite simple and suitable only for two dimensional drawings that are composed of lines, arcs, circles, and points. IGES is more powerful and used for translation of complex three-dimensional drawings.

So what is the best approach for a small shop to take?

### Consult with Your Customer

Consulting with your customer is probably the most important step. Your customer likes to know about your capabilities. In turn, you should know what the customer can offer to your shop, particularly when it comes to a drawing supplied on a disk or by email. Ask for a file format that your CAM software supports, preferably in the native format.

### Understand CAD/CAM Translators

If the translator has to be used, make sure you understand its capabilities and its limitations. Poor translators may not convert the original geometry, especially when it contains complex geometry such as splines.

### Train your CNC Programmer

Good CNC or CAD/CAM programmers can detect drawing flaws and mistakes, and often solve any problems quickly. They will also be able to eliminate geometry that is part of the drawing but not necessary to create the tool path. This skill might be one of the programmer’s most important skills.

### Educate Your Customer

Do not be afraid to tell the customers what you expect from them. They will understand that your requests are made in the spirit of producing their part within specifications as well as efficiently.

Yes, it seems that for many reasons true CAD/CAM convergence is not a part of small job shops. At the same time, there is nothing wrong with CAD and CAM working together well in this unique environment.

![](img/0023bd5cc50494e6d7799ab76d437c8d_33_0.png)

## Part Program Upgrading and Updating

*June 2004, updated February 2013*

Regardless of the methods used, developing a CNC part program does take time. Whether written manually or generated with the aid of a CAD/CAM system, a part program should not be considered as completed until it is used to run a few parts and optimized. Even the best part programmers cannot always predict every condition during actual machining. It is not unusual — in fact, it is very common — to see CNC operators make changes to the program at the control. If the program is perfect, no changes would be necessary, a situation that rarely happens.

Optimizing a part program means improving it, mainly for more efficient performance, but also for other reasons, such as change in setup, use of a different tool, or even improved safety. Optimizing a program can take place at the control (usually by the CNC operator) or away from the control (usually by the CNC programmer). Two terms are often associated with a program change — *program upgrading and program updating*.

### Program Upgrading

*Program upgrading* means strengthening the program, enriching it, and making it more cost effective without compromising quality of the part or safety of machining. When running several thousand parts in a batch or a job that repeats from time to time, upgrading part programs will have a profound effect on the overall cost of doing business. Shortening the cycle time by a few seconds can mean hours in overall savings. Here are some ideas that programmers and/or CNC operators can consider when upgrading an existing part program.

Programmed spindle speeds and cutting feedrates are the first items to evaluate; they require a very small intervention with virtually immediate improvement. It is a well-known fact that programmers take a rather conservative approach in this area. Another area of interest should be the clearances applied in the program — “cutting air” is never productive and should be minimized. Changing a grade of the cutting insert and increasing the feedrates also offer benefits without making major changes to the program. If the program contains various machining cycles, operators can make even more significant changes, depending on the cycle type.

One of the overall cycle time killers is excessive dwell time. The minimum dwell time is the amount of time required to complete one spindle revolution. In practice, this amount is often doubled to allow full revolution dwell at 50% of programmed spindle speed. For example, a programmed dwell time of one second for 1200 rpm spindle speed is excessive, yet often pro-

Good training combined with experience will reward every shop owner in a relatively short time. As a shop owner, try to provide your employees with quality training — it will pay off in no time.

![](img/0023bd5cc50494e6d7799ab76d437c8d_36_0.png)

## Lathe Cycles — To Use or Not to Use?

*July 2004, updated February 2013*

If we have to name a single major benefit that modern CNC technology has offered over the initial NC technology, it would have to be the various forms of machining cycles. Yes, those small routines save much of programmers’ time and calculations. CNC machining centers have had their ubiquitous G81, G82, G83, etc., for drilling, boring, tapping, and other operations related to hole machining for a long time. This group of special cycles makes perfect sense for the part programmer because even companies specializing in complex 3D can use them efficiently, albeit occasionally. Virtually every CAM software program supports these *fixed cycles* or *canned cycles*, as they are commonly called, through the post processor output. The story is somewhat different when it comes to CNC lathes and turning centers.

### Multiple Repetitive Cycles

In the early 1980s, Japanese company Fanuc adopted a concept long known to part programmers from the 1970s, who were using various programming languages, such the venerable Compact II, to develop roughing and finishing tool paths. The mathematical concept behind this development was quite simple — define the stock boundary, define the boundary of the finished contour, and the control will remove all the material contained within these two boundaries. The result of this adaptation of an early technology into a modern CNC turning system is now known under the collective umbrella of several *multiple*
