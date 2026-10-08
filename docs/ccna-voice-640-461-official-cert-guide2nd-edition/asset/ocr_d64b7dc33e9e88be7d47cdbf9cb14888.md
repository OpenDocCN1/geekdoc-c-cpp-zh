Table 6-4 Destination-Pattern Brackets Wildcard Examples
| Pattern | Description | Key Topic |
| --- | --- | --- |
| 555[1-3]... | Matched dials numbers beginning with 555, having 1, 2, or 3 as the fourth digit, and ending in any three digits. | |
| [14-6]555 | Matched dials numbers where the first digit is 1, 4, 5, or 6 and the last three digits are 555. | |
| 55[59]12 | Matched dials numbers where the first two digits are 55, the third digit is 5 or 9, and the last two digits are 12. | |
| ^[1-7].,[135] | Matched dials numbers where the first digit is 1–7, the second and third digits are any number, and the last digit is 1, 3, or 5. | |

These wildcards are most often used when creating dial-plans for PSTN access. Initially, the most logical destination pattern choice for the PSTN may seem to be 9T (for an outside line followed by any number of digits). The problem with this is that Cisco designed the T wildcard to match variable-length strings from 0-32 digits. When a user dials an outside number, such as 14085551212, the router configured with the T wildcard will sit silently and wait for the user to dial more digits. By default, the router will wait for additional dialed digits for 10 seconds, which is the interdigit timer (also called the T302 timer). Although you can force the router to process the call immediately after dialing the number by pressing the pound key (#), this is not something you would want to train all of your users to.

Creating a PSTN dialing plan using wildcards other than T is not extremely difficult, as long as you think through the reachable PSTN numbers. Table 6-5 provides a sample PSTN dial-plan that you could use in the United States.

Table 6-5 Sample PSTN Destination Patterns for North America
| Pattern | Description | Key Topic |
| --- | --- | --- |
| [2-9]...... | Used for 7-digit dialing areas | |
| [2-9].[2-9]...... | Used for 10-digit dialing areas | |
| 1[2-9].[2-9]...... | Used for 11-digit long-distance dialing | |
| [469]11 | Used for service numbers, such as 411, 611, and 911 | |
| 011T | Used for international dialing | |

**Note:** Although you can manually create an international dial-plan without using the T symbol, doing so can become tedious.

Example 6-12 illustrates the configuration of a North American PSTN dial-plan on a router. In this example, the T1 CAS port 1/0:1 is connected to the PSTN, and internal users must dial 9 for outside PSTN access.