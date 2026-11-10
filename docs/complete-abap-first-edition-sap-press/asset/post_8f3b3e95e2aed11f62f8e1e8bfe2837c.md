
To implement a mock object, you can take advantage of OOP by inheriting the real objects and redefining the methods to return dummy values. For example, if the method of the real object returns data from the database, you can redefine the method in the mock object to return some hard-coded values.

## 21.2.3 Writing and Implementing Unit Tests

To perform a unit test, we need to implement test classes. Test classes can be defined locally in the program or globally in Class Builder (Transaction SE24). To define a test class, we use the FOR TESTING addition with the CLASS DEFINITION statement. While defining a test class, we need to set certain properties, such as RISK LEVEL and DURATION. The system will use these properties to determine if the test class should be executed.

Listing 21.3 shows the syntax to define a test class.

```abap
CLASS lcl_test DEFINITION FOR TESTING
                             RISK LEVEL HARMLESS
                             DURATION SHORT.
ENDCLASS.
```

**Listing 21.3** Define Test Class

For RISK LEVEL, you can set the property as HARMLESS, DANGEROUS, or CRITICAL. The HARMLESS property indicates that executing the test class doesn’t affect any customizations or perform any database changes. The DANGEROUS property implies that the test class performs database changes. The CRITICAL property implies that the test class performs changes to customization and the database.

For DURATION, you can set the property as SHORT, MEDIUM, or LONG. The SHORT property implies that the test class runs fast and usually takes less than a minute to execute. The MEDIUM property implies that the test class takes anywhere from one to five minutes. The LONG property implies that the test class may take up to one hour to execute.

The RISK LEVEL and DURATION properties use client settings maintained via Transaction SAUNIT_CLIENT_SETUP, as shown in Figure 21.2.

The test class should implement at least one method with the FOR TESTING addition. The ABAP Unit framework provides a CL_ABAP_UNIT_ASSERT class, which contains static methods for the verification of test expectations.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_980_0.png)

Figure 21.2  Test Class Properties

In order to execute the test, we need to provide context for the test class. The context of a unit test is called a *fixture*. ABAP Unit executes certain predefined methods before executing the test method to prepare the system under test or to perform clean up after testing. We can use the fixture to prepare the components of the system under test or to load the test data.

There are two predefined methods called by ABAP Unit:

- **SETUP**  
  This method is called before each test within a test class. We can use this method to set up the required context for the test, such as test data.
- **TEARDOWN**  
  This method is called after each test within a test class. We can use this method to clear the context after each test.

Let's explain how to implement test classes with a working example. For this example, we'll use a class that provides the total tax due for each customer. The purpose of this class is to calculate the total tax amount that the customer is due. The class can be defined as shown in *Listing 21.4*.

```abap
CLASS lcl_account DEFINITION.
  PUBLIC SECTION.
    TYPES: BEGIN OF ty_customer,
             acc_no TYPE char5,
             tax_amt TYPE bseg-mwsts,
           END OF ty_customer.
    TYPES tt_customer TYPE STANDARD TABLE OF ty_customer.
    METHODS: set_customer IMPORTING im_customer TYPE tt_customer,
             get_tax_due IMPORTING im_acc_no TYPE char5 RETURNING VALUE(rt_tax_amt) TYPE bseg-mwsts.
  PRIVATE SECTION.
    DATA it_customer TYPE STANDARD TABLE OF ty_customer.
ENDCLASS.

CLASS lcl_account IMPLEMENTATION.
  METHOD set_customer.
    it_customer = im_customer.
  ENDMETHOD.

  METHOD get_tax_due.
    FIELD-SYMBOLS <fs_customer> LIKE LINE OF it_customer.
    LOOP AT it_customer ASSIGNING <fs_customer> WHERE acc_no EQ im_acc_no.
      rt_tax_amt = <fs_customer>-tax_amt.
    ENDLOOP.
  ENDMETHOD.
ENDCLASS.
```

**Listing 21.4** Class to Calculate Tax Due

In Listing 21.4, we defined a `get_tax_due` method, which imports the customer account number and returns the total tax due for the customer. We also implemented the `set_customer` setter method to initialize the customer table. For normal testing, this class would depend on data from the database to return the tax due for the customer, but ABAP Unit is all about eliminating these external dependencies.

The test class for this class can be defined as shown in Listing 21.5 to perform the test with some mock data.

```abap
CLASS lcl_test DEFINITION FOR TESTING
      RISK LEVEL HARMLESS
      DURATION SHORT.
  PRIVATE SECTION.
    DATA o_customer TYPE REF TO lcl_account.
    METHODS: setup,
             teardown,
             check_valid_tax FOR TESTING,
             check_invalid_tax FOR TESTING.
ENDCLASS.
```

**Listing 21.5** Test Class Definition

In Listing 21.5, we defined the LCL_TEST test class using the FOR TESTING addition and set the RISK LEVEL and DURATION properties. In the private section of the test class, we defined the O_CUSTOMER attribute as a reference object of the class under test.

We also defined the SETUP and TEARDOWN methods, which will be called automatically by ABAP Unit before it calls the CHECK_VALID_TAX and CHECK_INVALID_TAX test methods. We defined these test methods using the FOR TESTING addition. Note that we defined two test methods to ensure that the class under test is tested for both valid and invalid scenarios.

Listing 21.6 shows the implementation of the test class.

```abap
CLASS lcl_test IMPLEMENTATION.
  METHOD setup.
    TYPES: BEGIN OF ty_customer,
             acc_no TYPE char5,
             tax_amt TYPE bseg-mwsts,
           END OF ty_customer.
    DATA: lt_customer TYPE STANDARD TABLE OF ty_customer,
          lw_customer LIKE LINE OF lt_customer.
    lw_customer-acc_no = '1001'.
    lw_customer-tax_amt = '50'.
    APPEND lw_customer TO lt_customer.

    lw_customer-acc_no = '1001'.
    lw_customer-tax_amt = '80'.
    APPEND lw_customer TO lt_customer.

    lw_customer-acc_no = '1002'.
    lw_customer-tax_amt = '100'.
    APPEND lw_customer TO lt_customer.

    lw_customer-acc_no = '1002'.
    lw_customer-tax_amt = '200'.
    APPEND lw_customer TO lt_customer.

    CREATE OBJECT o_customer.
    o_customer->set_customer( lt_customer ).
  ENDMETHOD.

  METHOD teardown.
    CLEAR o_customer.
  ENDMETHOD.

  METHOD check_valid_tax.
    DATA lv_tax_amt TYPE bseg-mwsts.
    lv_tax_amt = o_customer->get_tax_due( '1001' ).
    cl_abap_unit_assert=>assert_equals(
      EXP = 130
      act = lv_tax_amt
      msg = 'Tax calculation is incorrect'
    ).
  ENDMETHOD.

  METHOD check_invalid_tax.
    DATA lv_tax_amt TYPE bseg-mwsts.
    lv_tax_amt = o_customer->get_tax_due( '2000' ).
    cl_abap_unit_assert=>assert_equals(
      EXP = 0
      act = lv_tax_amt
      msg = 'Tax calculation is incorrect'
    ).
  ENDMETHOD.
ENDCLASS.
```

**Listing 21.6** Test Class Implementation

For the implementation of the test class in Listing 21.6, we used the SETUP method to load some test data to the class under testing. We’re using the TEARDOWN method to clear the reference to the class under testing. This ensures that each test is performed with a new context.

Within the CHECK_VALID_TAX and CHECK_INVALID_TAX test methods, we're calling the GET_TAX_DUE method of the class under testing by passing different customer account numbers. We’re using the ASSERT_EQUALS static method of the CL_ABAP_UNIT_ASSERT class to compare the returned value with the expected value and show a message accordingly when the test is run.

Listing 21.7 shows the complete code example of the program we've discussed so far.

```abap
REPORT zdemo_abap_unit.
CLASS lcl_account DEFINITION.
  PUBLIC SECTION.
    TYPES: BEGIN OF ty_customer,
             acc_no  TYPE char5,
             tax_amt TYPE bseg-mwsts,
           END OF ty_customer.
    TYPES tt_customer TYPE STANDARD TABLE OF ty_customer.
    METHODS: set_customer IMPORTING im_customer TYPE tt_customer,
             get_tax_due IMPORTING im_acc_no TYPE char5 RETURNING VALUE(rt_tax_amt) TYPE bseg-mwsts.
  PRIVATE SECTION.
    DATA it_customer TYPE STANDARD TABLE OF ty_customer.
ENDCLASS.
```
