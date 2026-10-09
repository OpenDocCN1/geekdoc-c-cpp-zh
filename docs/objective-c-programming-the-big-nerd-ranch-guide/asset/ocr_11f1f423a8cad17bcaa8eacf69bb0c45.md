So when do you use Interface Builder and when do you set up views programmatically? Under simple circumstances, either will work. We could have built iTahDoodle's interface with a XIB. In general, however, the more complex your user interface, the more sense it makes to use Interface Builder.

(Now that you've seen more of Xcode, take a look at the tear-out card at the back of this book. This card contains keyboard shortcuts for navigating around Xcode. There are a bunch of them! As you continue with Xcode, use this card to find shortcuts that will save you time and clicks.)

# Making connections

Creating and configuring views is not all that you can do in Interface Builder. You can also connect, or “wire,” these view objects to your application’s code. In particular, you can set target-action pairs and assign pointers.

To the left of the layout grid is a list of “placeholders” and objects. This is called the document outline. (If you just see a stack of icons without labels, click the button to reveal the expanded list.)

Figure 28.10 Minimized and expanded document outline

![](bbox=[0.31, 0.47, 0.68, 0.77])

Find File's Owner under the Placeholders section of the document outline. A placeholder stands in for a particular object that cannot be specified until runtime. File's Owner stands in for whichever object will load this XIB as its user interface. In your case, File's Owner represents an instance of BNRDocument.

Now select the Insert button in the editor and Control-drag to File's Owner.