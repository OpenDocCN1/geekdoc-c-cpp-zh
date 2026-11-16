# 7.18 COMMENTING CONSTRUCTS

It's a good idea to include comments in a CLIPS program. Sometimes constructs can be difficult to understand, and comments can be used to explain to the reader what the constructs are doing. Comments are also used for good documentation of programs and will be helpful in lengthy programs.

A comment in CLIPS is any text that begins with a semicolon and ends with a carriage return. The following is an example of comments in the fire program:

```
;*********************************************************************
;*
;* Programmer: G. D. Riley *
;*
;* Title: The Fire Program *
;*
;* Date: 05/17/04 *
;*
;*********************************************************************
;
; Deftemplates
(deftemplate emergency "template #1"
    (slot type) ; What type of emergency
(deftemplate response "template #2"
    (slot type)) ; How to respond
; The purpose of this rule is to activate
; the sprinkler system if there is a fire
(defrule fire-emergency "An example rule" ; IF
    There is a fire emergency
    (emergency (type fire))
=>
    ; Activate the sprinkler system
    (assert (response
        (action activate-sprinkler-system))))
```

Loading these constructs into CLIPS and then pretty printing them will demonstrate that every comment starting with a semicolon is eliminated in the CLIPS program. The only comment that is retained is the one in quotes after the construct's name.

# 7.19 VARIABLES

Just as with other programming languages, CLIPS has variables available to store values. Variables in CLIPS are always written in the syntax of a question mark followed by a symbolic field name. Variable names follow the syntax of a symbol, with the exception that they must begin with a character. For good programming style, variables should be given meaningful names. Some examples of variables are: style