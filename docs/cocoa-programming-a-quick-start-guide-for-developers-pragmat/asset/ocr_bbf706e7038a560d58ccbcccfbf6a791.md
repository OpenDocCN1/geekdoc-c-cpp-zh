# # Key Value Observing

When I was a kid, we’d hope for snow days. These were days when it snowed so much that school was canceled and we could spend the day playing outside in the snow. Back then when it snowed, we’d listen to the radio or watch television for the list of school closings. We had to pick our school out of the list—the radio personality or TV weather man didn't know about us or which school we were listening for.

Now, with my daughter, things are different. We can still listen for school closings on radio and television, but we can also register with a local television channel’s website. Each year I go to the site and enter my email address and the specific school I’m interested in.

I’m registering as an observer. My email is on a list that is notified when the value of Cocoa Valley Schools changes from open to any other value. In this chapter, we’ll look at Key Value Observing (KVO), which is your Cocoa application’s version of the Observer pattern.

# ## 20.1 Codeless Connections

Let’s start this chapter with a basic application.

![](bbox=[0.377, 0.767, 0.547, 0.842])

On the left you have a stepper, and on the right you have a text field. As you click the top part of the stepper, the number in the text field increases by one at a time, and if you click the bottom part of the stepper, the number in the text field decreases.