
**TABLE 17-2 — Software Problems and Symptoms**

| Problem | Symptoms |
|---|---|
| Client software misconfigured | Client cannot connect, cannot receive an IP address, unable to browse the network |
| Improper passphrase entered | Client associated with the AP, but cannot log onto the wireless network; client connected to the wired LAN, but cannot place phone calls |
| DHCP server down | Client connects physically, but cannot acquire an IP address |
| RADIUS server down | Client associates with the AP, but cannot log onto the network when using a Robust Security Network (RSN) for a wireless LAN |

## Software Problems

Table 17-2 lists common software problems and their symptoms.

## Symptom, Diagnosis, and Solution

Because certain symptoms usually surface with specific problems, many issues can be resolved in a similar way to human health issues. Look at the symptom, identify the most likely cause (diagnosis), and then treat it (solution). Repeat this process until the problem is resolved.

### Symptom

Defining the symptoms means gathering information about the problem. What is happening? Where is it happening? What technology is involved? Which users, if any, are involved? Has it always been this way? Answering questions like these will help you determine the various details about the problem. Good questions are at the core of effective problem definition.

### Diagnosis

Based on the information gathered from your symptom analysis, what is the most likely cause, or what are the most likely causes? You can treat one or all, but you will most likely learn more by treating one cause at a time. Try one solution based on your diagnosis first and evaluate the results. This gives you expert knowledge over time or what some call “intuition.”

### Solution

The solution is the potential fix for the problem. You may try replacing a CardBus PC network card because you determine that, based on the symptoms, the most likely cause is a failed card. After replacing the card, you note that you are experiencing the same problem. Next, you may decide to try both cards in another machine that is currently using the same card model and is working. When you do this, both cards work in the other computer. Next, you may attempt to reload the drivers in the malfunctioning computer, but this doesn’t help either. In the end, you discover that the CardBus port is experiencing intermittent failures in the malfunctioning laptop. You send it to the vendor for repairs.

This illustration demonstrates the diagnosis and solution method—what I call the Adjust phase in my REACT methodology. You make changes and try different tactics until something solves the problem. You document the solution for future reference, but you also mentally document it. This is called experience, and as you get more of it you approach the level of expertise that helps you solve problems more quickly. For this reason, I look at problems as stepping-stones to a better future because solving this network or computer problem today will only make me more able to solve similar and different problems tomorrow.

## Systems Thinking

Now that we’ve covered four effective troubleshooting methodologies, we’ll look at an important concept that will make you a better troubleshooter. This concept is called systemss from a group of participants, and it attempts to remove some of the subjectivity through the process of averaging the participants’ responses.

Factors that impact voice quality include clarity, delay, and echo. Clarity is a perceptual measurement of an original sound compared with a digitized signal. Delay causes the perception of a continuous voice signal (like the continuous sound waves in a face-to-face communication) to be lost. Echo causes the voice signal to be reflected back toward the speaker. This echo can result in overlapping sounds and can reduce quality.

### Clipping

Clipping occurs when parts of the sound waves are lost during digital communications. This can occur as a result of many different problems:

- Processing overload on the encoder due to insufficient hardware
- Dropped packets between the sender and receiver due to media errors or other problems
- Overflows or underflows on the jitter buffer
- Network latency causing too much delay and forcing dropped packets
- Using a half-duplex speakerphone

When full-duplex speakerphones are used, they usually sample the environment to build a digital image of the noise floor within the area. This image is used to distinguish between a human speaker and the background noise. Half-duplex speakerphones do not do this and may interpret the background noise as a human speaking, which may in turn result in clipping.

Whatever the cause, remember that clipping is the loss of portions of sound within the digital stream of communications.
