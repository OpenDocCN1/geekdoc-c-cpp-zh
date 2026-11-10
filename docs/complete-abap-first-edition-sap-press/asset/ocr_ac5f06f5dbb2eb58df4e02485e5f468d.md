```
CLASS cl_encapsulation_demo IMPLEMENTATION.
  METHOD print.
    "Business logic goes here
  ENDMETHOD.
  METHOD set_copies.
    "Business logic goes here
    me->copies = copies.
  ENDMETHOD.
  METHOD get_counter.
    "Business logic goes here
    counter = me->counter.
  ENDMETHOD.
  METHOD reset_counter.
    "Business logic goes here
    CLEAR counter.
  ENDMETHOD.
  METHOD reset_copies.
    "Business logic goes here
    CLEAR copies.
  ENDMETHOD.
ENDCLASS.

CLASS c1 DEFINITION.
  PUBLIC SECTION.
    METHODS get_counter IMPORTING counter TYPE i.
  PROTECTED SECTION.
    DATA counter TYPE i.
ENDCLASS.
CLASS c1 IMPLEMENTATION.
  METHOD get_counter.
    DATA oref TYPE REF TO cl_encapsulation_demo.
    CREATE OBJECT oref.
    oref->reset_counter( ).
    oref->counter = counter.
  ENDMETHOD.
ENDCLASS.
CLASS c2 DEFINITION.
  PUBLIC SECTION.
    METHODS set_copies IMPORTING copies TYPE i.
  PRIVATE SECTION.
    DATA copies TYPE i.
ENDCLASS.
CLASS c2 IMPLEMENTATION.
  METHOD set_copies.
    DATA oref TYPE REF TO cl_encapsulation_demo.
    CREATE OBJECT oref.
    oref->reset_copies( ).
    oref->copies = copies.
  ENDMETHOD.
ENDCLASS.
```