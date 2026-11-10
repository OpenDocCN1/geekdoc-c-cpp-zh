```
EXCEPTIONS
  invalid_material. "Raised when material is invalid"
ENDCLASS.
```

**Listing 9.2** Maintaining Exception in Local Class

Having gone through how to handle procedural-based exceptions, next we'll shift our focus to class-based exception handling.

# 9.3 Class-Based Exception Handling

*Class-based exceptions* (object-oriented) help separate the exception handling logic from the main programming logic by handling the exceptions in a separate block. In the previous section on procedural methods for handling exceptions, you saw that beyond checking the system field `SY-SUBRC` to identify the exception, there isn't much information available about the exception.

In addition, because self-defined exceptions are supported only in function modules and methods, there's no proper way to handle error situations in regular programs. For example, if there's an error situation within a subroutine in which self-defined exceptions aren't supported, how do we handle it?

One way is to pass the error structure or some kind of variable in the parameter interface and check against it after the execution of subroutine, as shown in Listing 9.3.

```
PERFORM get_data USING v_matnr
                    CHANGING it_makt
                             retcode.

IF retcode IS INITIAL.
*Program logic
ELSE.
*Error handling logic
ENDIF.
FORM get_data USING p_matnr
              CHANGING pt_makt
                       p_retcode.
SELECT * FROM makt INTO TABLE pt_makt WHERE matnr EQ p_matnr.
IF sy-subrc IS NOT INITIAL.
  p_retcode = 1.
ENDIF.
ENDFORM.
```

**Listing 9.3** Error Handling in Subroutine