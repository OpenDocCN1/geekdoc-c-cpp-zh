Note: Notice that dial-peer tag 2000 is used on the CME. A router for a VoIP dial peer and used on the ROUTER B router for a POTS dial peer. This combination works just fine. The only restriction to keep in mind is that you cannot use the same dial peer tag value for different functions on the same router.

# Dial Peer Wildcards

As you saw in the previous few sections, configuring dial peers (and destination patterns) without using wildcards would be extremely time consuming. By far, the most commonly used wildcard is the dot (.), which represents any dialed digit. You will find a few wildcards useful in your configurations. Table 6-3 describes these wildcards.

| Table 6-3 Wildcards You Can Use with the destination-pattern Command |
| Wildcard | Description |
| --- | --- |
| Period (.) | Matches any dialed digit from 0–9 or the * key on the telephone keypad. For example, 20., matches any number from 2000 to 2099. |
| Plus (+) | Matches one or more instances of the preceding digit. For example, 5+23 matches 5523, 55523, 555523 and so on. This trend continues up to 32 digits, which is the maximum length of a dialable number. |
| Brackets ([]) | Matches a range of digits. For example, [1-3]22 matches 122, 222, and 322. You can include a caret (^) before the entered numbers to designate a "does not match" range. For example, [1-3]22 matches 022, 422, 522, 622, 722, 822, 922, and *22. |
| T | Matches any number of dialed digits (from 0–32 digits). |
| Comma (,) | Inserts a 1-second pause between dialed digits. |

Note: The pound symbol (#) on a telephone keypad is not a wildcard symbol. This key immediately processes a dialed number when it is entered without waiting for additional digits.

Tip: If you plan to create a dial peer using only the T wildcard as the destination pattern, Cisco recommends that you create the destination as .T. This requires a user to dial at least one digit to match the destination pattern. Otherwise, a phone left off-hook for for too long without a dialed digit will match the destination pattern.

Typically, the brackets wildcard is the most difficult to understand, primarily because it is the most flexible. Table 6-4 shows a few examples of how it can be used.