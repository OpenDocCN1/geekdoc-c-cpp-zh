Four more rules are necessary to analyze the remaining four possible states of a sensor. Each of the rules will be similar to the rule Normal-State, with the exception of the values retrieved from the sensor fact and the test CE used to determine the current state. All five of the state rules could be written as a single rule with an if expression on the RHS of the rule to determine the appropriate state of the sensor. This type of coding, however, defeats the purpose of a data-driven system. In addition, further modifications involving actions or conditions both or of a subset of the possible states would be made much more difficult by a single unwieldy rule. The remaining four state analysis rules are as follows:

```
(defrule TRENDS:High-Guard-Line-State
  ?s <- (sensor (raw-value ?raw-value&~none)
              (high-guard-line ?hrl)
              (high-red-line ?hrl))
  (test (and (>= ?raw-value ?hrl)
             (< ?raw-value ?hrl)))
=>
  (modify ?s (state high-guard-line)
          (raw-value none)))
```

```
(defrule TRENDS:High-Red-Line-State
  ?s <- (sensor (raw-value ?raw-value&~none)
              (high-red-line ?hrl))
  (test (>= ?raw-value ?hrl))
=>
  (modify ?s (state high-red-line)
          (raw-value none)))
```

```
(defrule TRENDS:Low-Guard-Line-State
  ?s <- (sensor (raw-value ?raw-value&~none)
              (low-guard-line ?lgl)
              (low-red-line ?lrl))
  (test (and (>= ?raw-value ?lrl)
             (<= ?raw-value ?lgl)))
=>
  (modify ?s (state low-guard-line)
          (raw-value none)))
```

```
(defrule TRENDS:Low-Red-Line-State
  ?s <- (sensor (raw-value ?raw-value&~none)
              (low-red-line ?lrl))
  (test (<= ?raw-value ?lrl))
=>
  (modify ?s (state low-red-line)
          (raw-value none)))
```