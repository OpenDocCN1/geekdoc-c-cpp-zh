only process the admission for science students. In order to make it work for any student category, we've maintained the important parameter of this method as a static type of the `cl_student` abstract class, from which the `cl_science_student` and `cl_commerce_student` classes inherit.

```
CLASS cl_student DEFINITION ABSTRACT.
  PUBLIC SECTION.
  METHODS tuition_fee ABSTRACT.
  METHODS get_fee ABSTRACT RETURNING VALUE(fee_paid) TYPE boolean.
  PROTECTED SECTION.
  DATA fee_paid TYPE boolean.
ENDCLASS.
CLASS cl_commerce_student DEFINITION INHERITING FROM cl_student.
  PUBLIC SECTION.
  METHODS tuition_fee REDEFINITION.
  METHODS get_fee REDEFINITION.
ENDCLASS.
CLASS cl_commerce_student IMPLEMENTATION.
  METHOD tuition_fee.
  "logic to calculate tuition fee for commerce students goes here
  "IF fee_paid.
      fee_paid = abap_true.
  ENDMETHOD.
  METHOD get_fee.
      fee_paid = me->fee_paid.
  ENDMETHOD.
ENDCLASS.
CLASS cl_science_student DEFINITION INHERITING FROM cl_student.
  PUBLIC SECTION.
  METHODS tuition_fee REDEFINITION.
  METHODS get_fee REDEFINITION.
ENDCLASS.
CLASS cl_science_student IMPLEMENTATION.
  METHOD tuition_fee.
  "logic to calculate tuition fee for science students goes here
  "IF fee_paid.
      fee_paid = abap_true.
  ENDMETHOD.
  METHOD get_fee.
      fee_paid = me->fee_paid.
  ENDMETHOD.
ENDCLASS.
CLASS cl_admission DEFINITION.
  PUBLIC SECTION.
  METHODS set_student IMPORTING im_student TYPE REF TO cl_student.
  METHODS enroll.
  PRIVATE SECTION.
  DATA admit TYPE boolean.
ENDCLASS.
```