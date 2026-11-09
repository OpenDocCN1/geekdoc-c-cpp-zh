
*repetitive cycles.*

Without a doubt, three of these cycles have become the staple of manual programming for CNC lathes since day one: the G71 cycle for roughing, the G70 cycle for finishing, and the G76 cycle for threading. Their ease of use (the user calculates only the finish contour points) and the possibility of operator changing the cutting parameters at the machine control have made them instant winners. The strongest feature of these cycles, brevity (only one or two blocks of program are required for roughing), also became their small disadvantage.

CNC lathe manufacturers and vendors have realized that they can offer a better price on their machines if they make the available memory smaller (CNC memory is very expensive even today). There are still many CNC lathes that have a very small memory storage capacity for the part programs, although that is changing rapidly.

Yet, even if the issue of capacity is becoming a non-issue, there is always the benefit of being able to change various cutting parameters at the control (depth of cut, for example). The developers of CAM software have realized this need and generally support the output of multiple repetitive cycles in the final program. What many developers also offer is the option of not choosing the cycles as the program output. Selection of this option will, of course, require a more robust memory capacity. It will also bring up an important question regarding *when not to use these cycles.*

### Cycle Programming

Cycles are nothing more than pre-programmed routines. They will define the tool motions strictly based on the criteria included in these internal routines. To be blunt (and somewhat unfair), the programmer is at the mercy of the software engineers who developed the control unit. Make no mistake about it. The control software was developed for most — but not all — turning, boring, or threading applications; it does the job extremely well in such situations. Logically, the software *could not* be developed for special applications.

Yet, programming is somewhat like sculpting. There is technology involved, there is skill involved, and there is strong individualism involved (called art in sculpting). In order to control every single tool motion exactly as planned, the programmer may find a particular cycle to be ineffective.

Take, for example, the G71 roughing cycle. It starts at the beginning of the cut and continues towards the end, with the change of direction allowed along the X-axis only. If your program requires frequent changes of cutting direction, the longer method (block-by-block) will be the choice. Single point threading cycle G76 is no different. It is great for a single start standard thread, but loses its appeal somewhat for multi-start threads (although it can still be used). It becomes virtually useless for special threads such as those with special forms, particularly when the threading bit is smaller than the thread itself or the thread shape has to be interpolated rather than formed.

Without a doubt, these multiple repetitive cycles have made the programming and machining jobs much easier for all of us. At the same time, we have to understand their limitations and the alternatives for situations when these cycles are not preferable or are even impossible to use efficiently. Apart from programming every tool motion manually (which is always an alternative), make sure your CAM system can handle the type of tool motions required by the work you do and your programmer can generate the critical tool path. Also make sure you have enough memory available in the control system to store these programs — they can be quite long. A DNC (direct numerical control) solution may help as well.

## Short Suggestions for Long Programs

*August 2004, updated February 2013*

Once in a while, your machine shop will face the need to run a CNC part program that exceeds the built-in control memory capacity. This method is commonly called DNC (direct numerical control) and uses the TAPE or EXTERNAL mode of the control panel rather than the more common MEMORY mode. Not much is required for this method to work with your CNC machine — a suitable software, a desktop or a laptop computer, a connecting cable and some configurations. If all goes well, you are up and running in no time; if not, read on for some suggestions.

For the purpose of this column, I define the term *long program* as a part program that cannot be executed from the control memory. The most common source of such programs is a CAD/CAM system processing complex machining operations. Although the majority of long programs involve some 3D machining (for example, mold work and multi-axis toolpaths), there is a growing need for more control of 2D toolpaths, for example, in pocketing or at high speeds. High quality CAD/CAM software offers a multitude of toolpaths and pocketing styles. When combined with control of the cutting width and depth, size of the part, cleanup of corners, ramping, etc., it is not unusual to end up with a long program. The main difficulty when running such a program is when the CNC operator has to *restart* the cut somewhere in the middle of the program, after a substantial tool path had been completed with a particular tool. Often, the main reason is a tool breakage.

Most CNC machines do not have *program restart* or *sequence return* features which address this problem. Yet, there are a number of ways the CAD/CAM programmers can minimize the downtime associated with interruption of the long program. Let’s look at some possibilities to consider:

### Computer Location

Locate the computer that sends the long program as close as possible to the CNC machine that receives it. As a rule, the computer that receives the data (CNC) must be ready *before* the computer that sends the data (desktop or laptop). That means a bit of running between the two that can be eliminated.

### Program Sections

This topic is a very important consideration. Each tool used in the program is automatically a separate section. However, sections for a single tool, especially a tool that does a lot of work, should be carefully defined as well. One technique that can be used is homing the machine (machine zero return) after each section has been completed, particularly along the Z-axis, then starting at the next section with the same tool. As these extra motions add to the cycle time, they should be preceded with a slash (block skip function). An addition of program stop (M00) or optional program stop (M01) to this method may offer additional benefits.

### Program Editor

Use a dedicated CNC editor (designed for CNC files) or a text editor that can highlight individual addresses in the program — for example, all Z-axis motions in red. Colors help to identify individual sections, and the editor can also be used to create a temporary copy of a shortened program.

### Block or Sequence Numbers

They do help a lot. Although blocks or sequence numbers add to the overall length of the program, this length is irrelevant in DNC operations. If a tool breaks, the sequence number at the time of interruption offers some information that can be used for restart. Instead of using block numbers for each block, consider using only a few block numbers in strategic places within the program. A good place for selective block numbers is at the beginning of every new section that uses the same tool, or at home position.

### Descriptive Comments

Identify individual operations or sections of the program. For example, if the same tool is used for roughing five pockets, place a comment at the beginning of each pocket tool path with a unique description.

### Feed and Retract Planes

Be consistent in selecting the Z-axis positions for the start of cut and retract when the cut is completed. Text editors can be used to search and/or replace common data.

### Cutting Feedrates

If you make the plunging feedrate different from the cutting feedrate, you will more easily find the beginning of a section from which the change can be done, just by searching for the feedrate. Also, you will not accidentally forget a feedrate or use the wrong one.

What else is there to watch for? The above suggestions can be applied individually, or combined. The most important is to make sure that any change implemented is a safe change. Watch for XY tool locations, missing spindle speeds and feedrates, the status of switches on the control panel, offset settings, and other related subjects.

Running a long program from an external computer in DNC mode can be very simple and uneventful. On the other hand, if problems do arise, be prepared to deal with them via good planning in order to minimize the undesired downtime.
