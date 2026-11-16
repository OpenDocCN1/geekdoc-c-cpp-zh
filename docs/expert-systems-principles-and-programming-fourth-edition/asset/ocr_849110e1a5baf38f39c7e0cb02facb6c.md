```
?trend <- (sensor-trend
(name ?sensor) (state ?state)
(end ?end-cycle-&?time))
(sensor (name ?sensor)
(state ?new-state-&?state)
(raw-value none))
=>
(modify ?trend (start ?time)
(end ?time)
(state ?new-state)))
```

The first pattern of both rules establishes the cycle. The next pattern finds the sensor-trend fact for the previous cycle. The constraint on the end slot ensures that the rules do not endlessly loop. For the rule State-Has-Not-Changed, the next pattern checks that the state from the previous cycle is the same as the state for the current cycle. The constraint ?new-state-&?state in the rule State-Has-Changed performs exactly the opposite test, making sure that the state has changed from the last cycle. Checking that the raw-value slot is the literal none prevents the trend from being determined before the present state of the sensor is determined. In both rules the end cycle time is updated. If the state has changed, then the state value and start cycle time must be updated as well.

# Issuing Warnings

The final phase of the cycle is the warnings phase. Three types of actions must be handled during this phase: sensors that have entered a red line region will have their associated devices shut off, sensors that have stayed in the guard line region for a specified number of cycles will have their associated devices shut off, and sensors that are in the guard line region and did not have their associated devices shut off will have a warning issued.

The following rule shuts off sensors that have entered a red line region:

```
(defrule WARNINGS::Shutdown-In-Red-Region
(cycle ?time)
(sensor-trend
(name ?sensor)
(state ?state&high-red-line | low-red-line))
(sensor (name ?sensor) (device ?device))
?on <- (device (name ?device) (status on))
=>
(printout t "Cycle " ?time " - ")
(printout t "Sensor " ?sensor " in "
?state crlf)
(printout t " Shutting down device "
?device crlf)
(modify ?on (status off)))
```