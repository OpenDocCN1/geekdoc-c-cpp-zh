# # MODIFYING THE TEMPLATE

![](bbox=[0.049, 0.159, 0.309, 0.49])

![](bbox=[0.339, 0.159, 0.605, 0.49])

![](bbox=[0.632, 0.159, 0.908, 0.49])

FIGURE 1.17 Setting the Background attribute

FIGURE 1.18 Setting the Type attribute

FIGURE 1.19 Selecting the Object library

OK, enough chatter. Let's start building something new. We're going to add a label to the main view that will display a short message. We will also add a text box to the flipside view, letting the user change this message. So, let's get started.

# ## MODIFYING THE MAIN VIEW

Open MainStoryboard.storyboard again, and zoom in on the main view controller scene. The background is a little too dark for my taste. Select the View object, and then switch to the Attributes inspector. Change the Background attribute to Light Gray Color (Figure 1.17). Next, select the info button and change its Type setting to Info Dark (Figure 1.18).

Now we need to add a label. Xcode makes it easy to add user interface objects. Just drag the desired object from the Library pane (the bottom half of the Utilities area) and drop it onto the scene. Make sure the Object library is displayed (cube icon second from the right in the library selector bar) (Figure 1.19), and scroll so the Label object is visible. Click the Label object and drag it from the Library pane to the main view controller scene's view.