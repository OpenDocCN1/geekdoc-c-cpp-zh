construct (which will be placed in its own module to create a reusable software component):

```
```
(defmodule OAV (export deftemplate oav))

(deftemplate OAV::oav
   (multislot object (type SYMBOL))
   (multislot attribute (type SYMBOL))
   (multislot value))
```
```

Using this deftemplate, some of the facts required by the IF portion of the preceding MYCIN rule would be:

```
```
(oav (object organism)
     (attribute stain)
     (value gramneg))

(oav (object organism)
     (attribute morphology)
     (value rod))

(oav (object patient)
     (attribute is a)
     (value compromised host))
```
```

MYCIN also associates with each fact a certainty factor (CF) that represents a degree of belief in the fact. The certainty factor ranges from -1 to 1; -1 means the fact is known to be false, 0 means no information is known about the fact (complete uncertainty), and 1 means the fact is known to be true.

Since CLIPS does not handle certainty factors automatically, this information must also be maintained. To do this, an additional slot in each fact will be used to represent the certainty factor. The oav deftemplate for each fact now becomes:

```
```
(deftemplate OAV::oav
   (multislot object (type SYMBOL))
   (multislot attribute (type SYMBOL))
   (multislot value)
   (slot CF (type FLOAT) (range -1.0 +1.0))))
```
```

and the examples facts might be:

```
```
(oav (object organism)
     . (attribute stain)
     . (value gramneg)
     . (CF 0.3))
```
```