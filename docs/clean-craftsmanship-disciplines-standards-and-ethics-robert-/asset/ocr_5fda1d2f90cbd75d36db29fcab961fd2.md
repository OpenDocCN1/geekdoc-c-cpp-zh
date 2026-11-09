# Continuous Build

Clearly, if you are going to deploy in short cycles, you have to be able to build in short cycles. If you are going to deploy continuously, you have to be able to build continuously.

Perhaps some of you have slow build times. If you do, speed them up. Seriously, with the memory and speed of modern systems, there is no excuse for slow builds. None. Speed them up. Consider it a design challenge.

And then get yourself a continuous build tool, such as Jenkins, Buildbot, or Travis, and use it. Make sure that you kick off a build at every push and do what it takes to ensure that the build never fails.

A build failure is a red alert. It’s an emergency. If the build fails, I want emails and text messages sent to every team member. I want sirens going off. I want a flashing red light on the CEO’s desk. I want everybody to stop whatever they are doing and deal with the emergency.

Keeping the build from failing is not rocket science. You simply run the build, along with all the tests, in your local environment before you push. You push the code only when all the tests pass.

If the build fails after that, you’ve uncovered some environmental issue that needs to be resolved posthaste.

You never allow the build to go on failing, because if you allow the build to fail, you’ll get used to it failing. And if you get used to the failures, you’ll start ignoring them. The more you ignore those failures, the more annoying the failure alerts become. And the more tempted you are to turn the failing tests off until you can fix them—later. You know. Later?

And that’s when the tests become lies.

With the failing tests removed, the build passes again. And that makes everyone feel good again. But it’s a lie.

So, build continuously. And never let the build fail.

# Relentless Improvement