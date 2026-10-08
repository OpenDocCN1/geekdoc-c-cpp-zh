6. What is the correct order of processing during a Mobile Connect call, if the caller has dialed the user's IP phone number?

+   a. Remote Destination, Remote Destination Profile, Ring Schedule, Access List
b. Remote Destination Profile, Remote Destination, Ring Schedule, Access List
c. Access List, Ring Schedule, Remote Destination Profile, Remote Destination
d. Ring Schedule, Access List, Remote Destination, Remote Destination Profile

7. Which component is not part of a Mobile Voice Access configuration?

+   a. Cisco Unity Connection Auto-Attendant
b. Cisco IOS H.323 VXML gateway
c. Mobile Voice Access Media Resource
d. End user configured for Mobile Voice Access

8. How does an H.323 gateway route calls inbound for the MVA service to the CUCM server hosting the service?

+   a. One dial peer matching the MVA access PSTN server.
b. Two dial peers: One matching the MVA access PSTN number with incoming called-number configured, and one matching the MVA access PSTN number pointing to the CUCM server.
c. A static route redirecting all HTTP calls to the CUCM server.
d. All H.323 configuration is dynamically created by the CUCM server via TFTP download.

9. Which IOS dial peer configuration command associates the dial peer matching the MVA access PSTN number with the VXML application hosted by the CUCM server running the MVA service?

+   a. incoming called-number 40855555000
b. session target ipv4:10.1.1.1
c. service mva
d. service mva http://10.1.1.1:8080/cmmivr/pages/IVRMainpage.vxml