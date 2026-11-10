```
FORM update.
*Check user authorization
CALL FUNCTION 'ZUSER_SOME_AUTH'
EXPORTING
  user = sy-uname
IMPORTING
  auth = lv_auth.
*Business logic
IF lv_auth EQ abap_true.
*Prepare for update
ELSEIF lv_auth EQ abap_false.
*Do something else
ENDIF.
*Ask user for confirmation
CALL FUNCTION 'POPUP_TO_CONFIRM'
*Business logic
CASE user_response.
WHEN 'Y'.
  "Update data
WHEN 'N'.
  "Cancel
WHEN others.
  RETURN.
ENDCASE.
ENDFORM.
```

**Listing 21.1** Typical ABAP Logic

**Listing 21.1** implements the logic to check user authorizations and updates the data in the database accordingly. In this program, you want to test how the program behaves when the authorization fails or when the user doesn’t confirm the data update. However, with the way the code is implemented, you need an actual user to check the authorizations or to respond to the confirmation pop-up.

These are the examples of *dependencies*; in this case, the program is depending on the user to provide inputs. Similarly, if the program reads a database table to check some settings, then we can say the program is dependent on the availability of actual data in the database to perform a test. We can’t implement TDD for a program that has such dependencies.

To implement TDD, we need to remove the dependencies of the program, such as the dependency on the user or database in our example. One way to do so is to follow the *separation of concerns* approach to development in which you don’t burden one program with carrying out all the activities; instead, you implement different classes to carry out different activities. In our example, instead of