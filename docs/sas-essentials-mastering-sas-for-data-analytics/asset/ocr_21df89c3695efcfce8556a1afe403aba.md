# TIPS AND TRICKS FOR RUNNING SAS PROGRAMS

TABLE 1.2 SAS Function Keys
| Function Key | SAS Command | Result |
|---|---|---|
| F2 | RESHOW | Resizes window interrupted by system command |
| F3 | END; /*GSUBMIT; BUFFER=-DEFAULT*/ / | Submits SAS statements in clipboard |
| F4 | RECALL | Recalls current SAS code to editor |
| F5 | PROGRAM (PGM) | Displays Editor Window |
| F6 | LOG | Displays Log Window |
| F7 | OUTPUT | Displays Output Window |
| F8 | ZOOM OFF; SUBMIT | Submits (runs) the current SAS program |
| F9 | KEYS | Displays this Keys Window |
| F10 | Not defined | |
| F11 | COMMAND BAR | Moves cursor to command bar |
| F12 | Not defined | |

A boundary line separates (parts) of a SAS program. The SECOND.SAS example note that a minus in a small box appears on the screen next to the KEYWORD DATA (and another one to PROC MEANS). Clicking on this box compresses the code to its first line, and is a way to temporarily hide sections of code. When you run the code, the program still “sees and acts upon” what is in the compressed section.

# 1.4.2 Using Function Keys

You can use keyboard keys to move from window to window or to execute certain tasks in SAS. Some people prefer the use of function keys (rather than mouse clicks) as a quicker way of selecting program options. Table 1.2 lists some of the SAS function keys that you can use throughout this.
You also customize these keys. To display the full set of function key commands, on the menu bar select Tools → Options → Keys.

# HANDS-ON EXAMPLE

In earlier examples, you cleared the information from the Log Windows manually. In this example, you will create a new F12 function key command that will clear the Log Window and the Results Window and return you to the Editor Window. The F12 key you’re about to define uses the SAS commands:

+   * CLEAR LOG – clears the contents of the Log Window.
* ODSRESULTS; CLEAR; – clears the contents of the Results window (and closes that). Note that there is no blank between ODS and RESULTS.
* PGWM – returns you to the PGWM (i.e. to the active window most recently edited).

Following these instructions shows how to create a new F12 function key definition. Table 1.2 shows some of the key definitions that appear on your screen.

(continued)