![](bbox=[0.147, 0.065, 0.852, 0.458])

**Figure 6-18** Configuring Dial Peers Using CCP

Unlike the POTS dial peer configuration window in CCP, the VoIP dial peer configuration does not have the wizard-based configuration items; it allows only the manual dial peer creation.

# # Understanding and Implementing CME Class of Restriction

If you implement what you've seen so far, you can create a powerful VoIP system that supports both internal (iphone) and external (dial peer) dialing. However, there might be times when you need to prevent some users from calling certain numbers, such as the following examples:

+   - Prevent standard employees from making international calls, but allow management to place international calls without restriction\- Block certain high-cost numbers (such as 1-900 numbers in the United States)
- Prevent certain internal phones from reaching executive office directory numbers

This list goes on and on, but you get the idea: it's necessary to place calling restrictions on the VoIP network. If you were implementing this feature in the full Cisco Unified Communications Manager (CUCM) platform, you would use a feature called Partitions and Calling Search Spaces (CSS). In the CME environment, the equivalent feature is called incoming and outgoing Class of Restriction (COR) lists.