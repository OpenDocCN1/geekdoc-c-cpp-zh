# CHAPTER 3

# # Bootstrapping

The first thing to do in any software project is to become familiar with the environment.

Because we are working with Bluetooth, it’s important to learn how to initialize the Bluetooth radio and report what the program is doing.

Both the Central and Peripheral talk to the computer over USB when being programmed. That allows you to report errors and status messages to the computer when the programs are running (Figure 3-1).

![](bbox=[0.009, 0.501, 0.987, 0.699])

**Figure 3-1. Programming configuration**

# ## Programming the Peripheral

It is useful to print out what nRF is thinking to make debugging easier, so this chapter will teach how to print data from the the nRF to the