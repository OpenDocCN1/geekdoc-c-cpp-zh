
## AN OVERVIEW OF DTRACE

DTrace lets you trace your application as it runs. Tracing is logging information about a running computer program for debugging and performance analysis; it is used mainly by developers. Contrast this with “high-level logging,” which is used by end users and system administrators to log program errors, exceptions, failed scripts, and so on.

Apple added DTrace support and debuted Instruments in Mac OS X 10.5. Instruments reduces the DTrace learning curve to manageable levels and makes a lot of traditionally difficult debugging tasks seem almost trivial by comparison.

In DTrace, a probe is a script to perform a specific task. In the glossy, graphic realm of Instruments, a probe (or collection of interrelated probes) is more generally referred to as an instrument. A probe is essentially a script that watches for specific events and records relevant information.

In the field of quantum mechanics, it’s been shown that the act of observing something changes its nature. This is true of profiling software as well. For example, adding a bunch of code to an application to track its performance will affect its performance. One of the most celebrated aspects of DTrace is its extremely minimal performance impact when a probe is enabled; and there is no impact for disabled probes. This means that for most developers, the act of tracing won’t have a noticeable impact on the application’s performance profile. Because of this, DTrace can be used on production systems without slowing them down.

TIP: You can run DTrace from the command line by using the dtrace command. Type man dtrace in the Terminal and press Return to learn more.

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_340_0.png)

## A TOUR OF INSTRUMENTS

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_341_0.png)

FIGURE 20.1 The template chooser sheet

An entire book could (and should) be dedicated to DTrace and Instruments. The long list of available instruments continues to grow, and many require a solid grasp of one or more debugging and profiling techniques. This section will use as examples the three most common tasks for which the typical developer would use Instruments. First, however, you’ll need to get familiar with Instruments’ user interface.

### AN OVERVIEW OF THE INSTRUMENTS USER INTERFACE

When you first launch Instruments, you’re given an empty document and prompted to choose a template for the trace document that Instruments will create for you. A template is one or more instruments configured in a particular way. Figure 20.1 shows the template chooser sheet with a number of templates. This sheet, like Xcode’s template chooser sheet, is broken down into categories: iOS, iOS Simulator, Mac OS X, and User (templates you’ve created and supplied).

> TIP: The trace operations you perform are done inside an Instruments trace document. A document contains the instruments and their configuration as well as every trace session recorded into it. It can be saved for later review, and future trace sessions can be appended to it.

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_341_1.png)

FIGURE 20.2 An Instruments trace document

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_342_0.png)

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_342_1.png)

Figure 20.2 shows a trace document with one 33-second trace session recorded in it. This document used the Time Profiler template found under the Mac OS X category of the template chooser. A great deal of information is shown here, with all of Instruments’ main views active.

TIP: The trace document can be saved and re-opened later. You can also append a new session by using the Record button.

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_343_0.png)

FIGURE 20.3 The Time Profiler showing multiple tracks

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_343_1.png)

FIGURE 20.4 Choosing another track

Figure 20.3 shows the expanded Time Profiler (using the disclosure triangle to the left of its name). The most recent track is always placed on top. Subsequent sessions will produce additional tracks for each instrument, and they can be reviewed and compared by expanding the disclosure triangle and clicking the track itself. The active track is shaded a darker blue (Figure 20.4).

There are many more view modes that won’t be covered in this chapter. Instead, let’s stick to the main views.

### THE TOOLBAR

There are some important clusters of controls on the toolbar you’ll need to understand. Let’s explore each major grouping, starting on the left side of the toolbar.

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_344_0.png)

The Record and Target controls work closely together. Use the Target control to attach Instruments to any running process. Depending on how you launched Instruments (see the “Launching Instruments” section, later in this chapter), a target (the application you’re tracing) may already be selected. Use the Record controls to control the trace. From left to right, there is a pause button to pause and resume tracing the running program; the Record button to start and stop recording new tracks; and a restart button, which stops the current trace and starts a new one (producing a new track). If the program is not running when the Record button is pressed, it will be launched. If the program was launched by the trace session, pressing the Record button while recording will stop recording and terminate the program.

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_344_1.png)

The Inspection Range controls specify the range of time in the track’s timeline you want to inspect. Specifically, you can filter out all trace information that is not within the specified range. The left button marks the beginning of the time you want to inspect; the right button marks the end. Setting a beginning point with no end means start here and show me everything to the end; setting an end point with no beginning means show me everything from the beginning up to this point. The middle button clears the selected range.

Though not part of the toolbar, it’s important to understand how to specify a point in time. You do this by dragging the scrubber control to the desired location in the timeline. The scrubber control is located in the graduated bar just above the instrument tracks. The term scrubber comes from audio/video applications, where the time-pointer control is moved or scrubbed across a track to view and listen to the scrubbed region of time.

The status control in the center of the toolbar shows (in hours, minutes, and seconds) the length of the current trace session (by default) or the currently displayed trace session and number of sessions in the document (if there’s more than one recorded) and provides controls (the left and right arrows) to switch between sessions. Click the small icon to the right of the time display to toggle between running time (the session’s length) and inspection time (the current position of the scrubber control).

The View controls toggle the three primary views in a trace document’s interface. From left to right, the buttons toggle the Instruments, Detail, and Extended Detail views. You’ll explore them in a moment.

The Library control toggles the Library panel (Figure 20.5), which provides all available instruments. To add a new instrument to the trace, drag it from the Library panel and drop it into the Instruments list.

The Search control filters the displayed trace information by symbol or library (to choose the filter, click the magnifying glass icon in the control’s left edge and select from the menu). For example, typing “drawRect” into the field will show only the trace information about the -drawRect: method provided by NSView (and any other methods containing “drawRect” in their names), assuming it’s been called during the recorded trace session.

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_345_0.png)

FIGURE 20.5 The Library panel

FIGURE 20.6 The Strategy bar

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_346_0.png)

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_346_1.png)

FIGURE 20.7 The Status bar legend

### THE STRATEGY BAR

The Strategy bar (Figure 20.6) is new in Instruments 4. It gives you three main tracing strategies to choose from. The buttons on the left edge of the bar toggle between the (from left to right) CPU, Instruments, and Threads strategies. (All the figures in this chapter thus far have shown the Instruments strategy—the default strategy in Instruments 4.) The pop-up menus let you filter by core, process, and thread. An additional pop-up appears in CPU and Threads strategies, letting you specify additional chart options.

The right-most button pops up a graphical legend (Figure 20.7) whose contents depend upon the chart mode (which colorizes the chart information). The legend shows each color used and what it represents in the chart.

Figure 20.8 shows the trace session from Figure 20.3 using the CPU strategy. The application’s activity is divided according to the CPU core on which that activity took place. If you have more than one instrument in the Instruments list, use the pop-up below the Instruments list to switch between them and see their collected trace information (Figure 20.9).

Figure 20.10 again shows the same trace session, this time using the Threads strategy. Here, the application’s activity is divided by thread (if you’re running Mac OS X 10.6 or later, you may see many threads here that you never knew were created).
