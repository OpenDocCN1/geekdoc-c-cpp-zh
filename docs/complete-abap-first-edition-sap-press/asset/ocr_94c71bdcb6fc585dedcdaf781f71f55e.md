The attribute `message` holds the message that can be set by calling the `set_message` method. The notification is displayed by calling the `display_notification` method. In this class, all of the components have public visibility.

Because all of the components are visible outside the class, any change to them will break the implementation in all the apps that use this API. For example, implementing additional features such as filtering a message or restricting the number of messages per app may be difficult with this design.

The `set_message` setter method is provided to set the message after screening it (such as screening for inappropriate words). However, this restriction can be bypassed easily by third-party app developers, because the `message` attribute is also accessible from outside the class. Therefore, outside developers can directly access the attribute to set the message instead of calling the `set_message` method.

The API in Listing 8.15 can be enhanced by hiding the implementation, as shown in Listing 8.16.

```
CLASS cl_notification_api DEFINITION.
  PUBLIC SECTION.
  METHODS set_message IMPORTING im_message TYPE string.
  METHODS display_notification.
  PRIVATE SECTION.
  DATA message TYPE string.
  METHODS filter_message RETURNING VALUE(boolean) TYPE boolean.
  METHODS check_count RETURNING VALUE(boolean) TYPE boolean.
  METHODS check_status RETURNING VALUE(boolean) TYPE boolean.
ENDCLASS.
CLASS cl_notification_api IMPLEMENTATION.
  METHOD set_message.
    message = im_message.
  ENDMETHOD.
  METHOD display_notification.
    IF me->?filter_message( ) EQ abap_true OR
       me->check_count( ) EQ abap_true OR
       me->check_status( ) EQ abap_true.
      WRITE message.
    ELSE.
      CLEAR message.
    ENDIF.
  ENDMETHOD.
  METHOD filter_message.
*Filtering logic goes here and the parameter "Boolean" is set to
*abap_true or abap_false accordingly.
  ENDMETHOD.
  METHOD check_count.
```