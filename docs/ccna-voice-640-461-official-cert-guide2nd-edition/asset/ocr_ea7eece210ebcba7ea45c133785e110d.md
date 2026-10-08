This configuration creates two identical destination patterns for the two FXO ports. Because the preference command is not used to indicate a more preferred dial, the router will randomly choose one of the FXO ports as an exit anytime user dials 911 or 9911 (the additional 9 are entered if users are accustomed to dialing 9 for an outside line). The dial peers created for the 911 destination pattern (dial peers 10 and 12) are also assigned the no-digit-strip command. Otherwise, the automatic digit-stripping rule of POTS would strip explicitly defined digits (which are all of them in this case; the router would not send any digits to the PSTN). The dial peers created for the 9911 destination pattern (dial peers 11 and 13) are assigned the forward-digits 3 command to send the right-justified three digits (911, in this case) to the PSTN and allow the automatic digit-stripping rule to remove the initial 9 access code.

# Practical Scenario 4: Using Translation Profiles

The digit manipulation discussed thus allow you to perform "minor translations" to a number. For example, you can add some digits to ensure digits do or not get stripped with the forward-digits command. The num-exp command allows you to make the biggest changes of all, but these changes are applied globally to the router, which might not give you the flexibility all situations require. Translation profiles are useful to address these needs. If you find yourself saying, "I want to change this dialed number to that dialed number, but only when it goes out this port," you need a translation profile.

Working with translation profiles is definitely not as easy as working with the "simple" digit manipulation methods discussed earlier. Implementation of translation profiles requires a three-step process:

+   **Step 1.** Define the rules that dictate how the router will transform the number.

+   **Step 2.** Associate the rules into a translation profile.

+   **Step 3.** Assign the translation profile to a dial peer.

In a way, this is similar to access-list configuration on a router.

To demonstrate the configuration of translation profiles, consider the scenario illustrated in Figure 6-15.

The headquarters of this organization used the DID from a PSTN provider of 602.555.XXX. This allows PSTN callers to dial directly into the organization without being redirected by a receptionist. Typically, when you lease a block of DID numbers, the PSTN carrier will strip the numbers to a four-digit extension. In this case, the DID block assigned to the organization (6XXX) does not match its internal extension range (5XXX). The administrator of network would like to translate all 6XXX dialed numbers to 5XXX, but only if these dialed numbers come in from the T1 PSTN interface, so as to interfere with the numbering scheme of the remote office. To accomplish this, he cannot use the num-exp 6... global configuration command because it will interfere with dialing the 6XXX extensions at the remote office. This situation is ideal for translation profiles.