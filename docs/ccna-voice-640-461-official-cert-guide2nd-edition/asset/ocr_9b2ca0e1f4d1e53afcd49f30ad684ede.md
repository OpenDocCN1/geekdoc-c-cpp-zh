```
primary-ni National ISDN Switch type for the U.S.
primary-ntt NTT switch type for Japan
primary-qsig QSIG switch type
primary-ts04 TS04 switch-type-primary for Australia (obsolete)
CME_Voice(config)# isdn switch-type primary-5ess
CME_Voice(config)# controller t 1/0
CME_Voice(config)# pri-group?
fas_d Specify the operation of the D-channel timeslot.
service Specify the service type
timeslots List of timeslots in the pri-group
<cr>
CME_Voice(config-controller)# pri-group timeslots?
<1-24> List of timeslots which comprise the pri-group

CME_Voice(config-controller)# pri-group timeslots 1-24?
fas_d Specify the operation of the D-channel timeslot.
service Specify the service type
CME_Voice(config-controller)# pri-group timeslots 1-24
CME_Voice(config-controller)*Z
CME_Voice# show voice port summary
```

| PORT CH SIG-TYPE ADMIN OPER STATUS EC |
|---|---|---|---|---|---||
| 1/0:23 | 01 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 02 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 03 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 04 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 05 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 06 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 07 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 08 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 09 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 10 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 11 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 12 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 13 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 14 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 15 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 16 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 17 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 18 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 19 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 20 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 21 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 22 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 23 | isdn-voice | up | dorm | none | y |