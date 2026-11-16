slot and the <upper-limit> term indicates the maximum value for the slot. ?VARIABLE indicates that there is either no minimum or no maximum value (depending on whether it is first or second). For example, the age slot in the person deftemplate can be modified to prevent negative values from being placed in the slot:

```
(deftemplate person
    (multislot name (type SYMBOL))
    (slot age (type INTEGER) (range 0 ?VARIABLE)))
```

If we're willing to assume that no one lives beyond 125 years, then the range attribute could be changed to (range 0 125). As with the allowed value attributes, the range attribute does not restrict the type of a slot value to being numeric. It restricts only the allowed numeric values of a slot to the specified range if the slot's value is numeric. The default range attribute for slots is (range ?VARIABLE ?VARIABLE).

# The Cardinality Attribute

The cardinality attribute allows the specification of the minimum and maximum number of values that can be stored in a multislot. The general format of the cardinality attribute is (cardinality <lower-limit> <upper-limit>), where <lower-limit> and <upper-limit> are either ?VARIABLE or a positive integer. The <lower-limit> term indicates the minimum number of values the slot can contain and the <upper-limit> term indicates the maximum number of values the slot can contain. ?VARIABLE indicates that there is either no minimum or no maximum number of values the slot can contain (depending on whether it is first or second). The default cardinality attribute for a multislot is (cardinality ?VARIABLE ?VARIABLE). The following deftemplate could be used to represent company volleyball teams, which must have six players and may have up to two alternate players. Note that type, allowed value, and range attributes are applied to every value contained in a multislot.

```
(deftemplate volleyball-team
    (slot name (type STRING))
    (multislot players (type STRING)
                 (cardinality 6 6))
    (multislot alternates (type STRING)
                 (cardinality 0 2)))
```

# The Default Attribute

In previous chapters each deftemplate fact that was asserted always had an explicit value stated for every slot. It is often convenient to automatically have a specified value stored in a slot if no value is explicitly stated in an assert command. The default attribute allows such a default value to be specified. The general format of the default attribute is (default <default-specification>), where <default-specification> is either ?DERIVE, ?NONE, a single expression (for a single-field slot), or zero or more expressions (for a multifield slot).