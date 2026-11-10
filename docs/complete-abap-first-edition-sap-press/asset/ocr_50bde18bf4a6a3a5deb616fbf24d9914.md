```
```text
CLASS cl_admission IMPLEMENTATION.
  METHOD set_student.
    IF im_student->get_fee( ) EQ abap_true.
      admit = abap_true.
    ENDIF.
  ENDMETHOD.
  METHOD enroll.
    IF admit EQ abap_true.
*Perform the steps to enroll
    ENDIF.
  ENDMETHOD.
ENDCLASS.

DATA : commerce_student TYPE REF TO cl_commerce_student,
       science_student TYPE REF TO cl_science_student,
       admission TYPE REF TO cl_admission.
START-OF-SELECTION.
CREATE OBJECT: commerce_student,
               science_student,
               admission.
CALL METHOD commerce_student->tuition_fee.
CALL METHOD admission->set_student( EXPORTING im_student = commerce_
student ).
CALL METHOD admission->enroll.

CALL METHOD science_student->tuition_fee.
CALL METHOD admission->set_student( EXPORTING im_student = science_
student ).
CALL METHOD admission->enroll.
```
```

Listing 8.29  Code for Dynamic Call Method Binding

When the set_student method of the cl_admission class is called, it allows us to pass any student object that is inherited from cl_student. Within this method, we're checking if the student has paid the fee by calling the get_fee method of the imported object and accordingly processing the admission of the student. Here, even though the static type of the imported object is different from the static type of the importing parameter, the system automatically binds the object to the correct instance.

With this design, we can easily process admissions for any future student category via the cl_admission class. All the student category class needs to do is to inherit the abstract class cl_student.