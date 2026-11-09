
program must work in both cases to your satisfaction.

## Example: Two Face Cuts

There are other applications of a block skip, such as programming a test cut for precise offset settings or programming two or more face cuts for a part with variable stock height or length. The next example shows two face cuts — the first one may be skipped if there is no need for it:

```
...
N78 G90 G00 X-3.0 Y2.65
/N79 Z0.1 M08
/N80 G01 X8.5 F15.0
/N81 G00 Z0.2
/N82 X-3.0
N83 Z0 M08
N84 G01 X8.5 F12.0
N85 G00 Z1.0
...
```

Although the M08 function could have been programmed earlier than in block N79, the program segment as shown serves as an example of necessary repetition in block N83.

## Using the Forward Slash

Several general rules apply to using the forward slash in the program. Normally, the slash symbol must always be the first character in the block. Some controls allow block skip in the middle of a block, a feature that offers additional possibilities. This is not a standard feature, so check it first. Another rule is aimed at the CNC operators. Be sure to activate the switch *before* the first slash in the program is processed, and deactivate the switch only *after* the last block with the slash had been processed. Following these simple rules will make the Block Skip command a valuable addition to the current programming methods by adding flexibility at the machine.

![](img/0023bd5cc50494e6d7799ab76d437c8d_111_0.png)

## Simulating the Toolpath

*October 2006, updated February 2013*

Any skilled CNC programmer and operator should be able to interpret and check the part program in its written form. Although time and experience will make such interpretation faster and more accurate, scrolling through a rather dry program code cannot beat a real visual simulation of the toolpath on a computer screen.

### Types of Toolpath Simulation

Currently, there are several types of toolpath simulation available. One is built right into the control system, by the manufacturer, typically as an option at an added cost. Another type is an integral part of CNC oriented software, such as Mastercam, Edgecam, and most others.

For those machine shops that have only standard controls and no programming software, there is an attractive *stand-alone* alternative — toolpath simulation software that runs on a desktop or a laptop computer. Two common types of this group are 1) a wireframe simulation and 2) a simulation using a shaded model. Current software market offers a number of choices that vary greatly in features (and prices). Virtually all software vendors offer a time-limited trial period, which lets interested users test several software packages before purchasing the right one for their needs. Although the initial cost of the software is always important, its actual features and capabilities are much more critical, particularly in the long term.

All simulation software available today is expected to support the common tool motions, fixed cycles for machining holes, and several other common control features. Most have a built-in text editor that can be used to write and edit the part program. Unfortunately, a lot of software programs of this type lack many control system features and attention to detail. When selecting CNC simulation software, ask questions important to you and to your common work, before committing to a purchase. Does the software support milling and turning operations in one package? Does it support special functions of the control system? For example, you may have *Coordinate Rotation* or *Programmable Mirror Image* functions that you use frequently, but cannot simulate them because the software does not provide the necessary support. Fanuc control support is generally standard for most simulation software, but does the software provide its variations, such as for Haas or Mitsubishi controls? What about *User Macros*? *Vertical lathes*? DNC? The list of these and similar questions can be quite long and it would take more than a short essay to cover all details. To offer at least some insight in the search of the perfect simulator, I will use my own experience as an example.

### What I Want in a Simulator

My quest has been for a CNC toolpath simulator that I would want to include in one of my books (on a CD). I have evaluated over a dozen CNC simulation software packages. My goal was to find one that is user friendly, features rich, and affordable—a combination rather rare these days. Simulators using a shaded model were visually attractive, but the additional requirement of stock and tool definitions did not suit my needs for general use. Furthermore, I often did not find support of the software for many of the special functions that my in-depth CNC books cover, features I wanted to be simulated on the screen. I wanted simplicity, accuracy, and features—a lot of features.

Eventually, my long quest ended when I found (www.ncplot.com) a Michigan-based company offering software called *NCPlot*. Its version 2.0 was a relative newcomer to the market; the newest version is *NCPlot v2*.

What I like about *NCPlot* is what I also believe many machine shops will find very useful as well. The complete list can be quite long, so I will mention some of the main features that can be used as a general guide for selection of any CNC simulation software currently on the market. In NCPlot, once you select the machine type (there are many customizable modes), the software interface is easy to navigate and selections are clearly defined.

*NCPlot* supports CNC mills and machining centers, including 4-axis machining centers. It also supports CNC lathes, including vertical lathes (right and left orientation). It even supports special variations between controls types, such as different subprogram formats. You can write the part program from scratch, using the full-featured built-in text editor (amazingly, it even renumbers Ps and Qs in lathe cycles), or you can import a DXF file from a CAD software to generate a toolpath.

Support for all basic tool motions, fixed cycles for machining holes, and clean graphic display with zooming, rotation, and panning is to be expected as bare minimum for this kind of software, but *NCPlot* goes much further. Its support for control options such as *Polar Coordinates*, *Scaling*, *Coordinate Rotation*, *subprograms* in many formats, G71-G73 type lathe cycles, *automatic corner breaking*, *DXF* input and output, and a whole lot more is first class. Add to it a full support for Fanuc macros (including compatible controls), macro expression calculator, even *Visual Basic* scripting, and you have software from a relatively small company that can challenge the big guys any day. Congratulations to Scott Martinez of *NCPlot* — keep on the great work.

The best part of *NCPlot* is its expected price. Back in 2006, the original version, for all these features and many more super-features, was under $300 (including a forum support and discount pricing for multiple purchases). Several years later, the price for the most recent version remains at $299. The combination of features and price of *NCPlot* v2 seems to be unbeatable. Every machine shop has its own needs and unique requirements. When it comes to simulation software, you may decide to use *NCPlot* as the software of choice, or as software for the purpose of shopping comparison. Either way, an intelligent selection will result in both a better working environment and CNC programs that reach the machine in much better shape. Let the example of my own needs serve as a path to your particular requirements.

![](img/0023bd5cc50494e6d7799ab76d437c8d_114_0.png)

## Automatic Corner Breaking

*November 2006, updated February 2013*

In a typical lathe work, there are many situations where the cut from shoulder to diameter — or from diameter to shoulder — requires a corner break. Breaking a sharp corner is a very common practice for eliminating burrs, providing clearances, and offering easier handling and assembly. It also improves appearance of the part.

### Size of Corner Breaks

Engineering drawings often specify that all sharp corners are to be broken, but do not always provide their size. It is up to the CNC programmer to make the selection, which may vary from 0.005 to 0.020 inches (0.125 to 0.500 mm) or even more for special applications. The required corner break is either a chamfer at 45 degree angle, or a blend radius (fillet). Many corner breaks apply to cuts between a shoulder and the adjacent diameter, where the cut takes a 90-degree turn in one axis at a time. Although the calculations of start and end points are not difficult, they can be time consuming if many corners are involved (shaft work with many diameters, for example).

### Programming Corner Breaks

Fanuc and similar controls provide a feature that greatly simplifies programming of such corners — it is called *Automatic Corner Breaking*. To better understand the difference in programming approach, compare the following examples. The first one shows a single chamfer of 0.1 between shoulder and diameter, calculated for each endpoint (blocks N5 and N6 make the chamfer):
