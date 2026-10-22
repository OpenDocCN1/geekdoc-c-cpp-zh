# Chapter 20

# Active Record Part III:
Object Life Cycle

So far we've looked at how to connect to Active Record, access data and attributes, and link together tables. This chapter rounds off our description of Active Record. It looks at the life cycle of Active Record objects; the validations and hooks that you can define affect how they are processed.

# 20.1 Validation

Active Record can validate the contents of a model object. This validation can be performed automatically when an object is saved. You can also programmatically request validation of the current state of a model. If validation fails when you're saving an object, the object will not be written to the database; it will be left in memory in its invalid state. This allows you (for example) to pass the object back to a form so the user can correct the bad data.

Active Record distinguishes between models that correspond to an existing row in the database and those that don't. The latter are called new records (the new_record? method will return true for them). When you call the save method, Active Record will perform a SQL insert operation for new records and an update for existing ones.

This distinction is reflected in Active Record's validation workflow—you can specify validations that are performed on all save operations and other validations that are performed only on creates or updates.

At the lowest level you specify validations by listing one or more methods names as symbols on calls to the validate, validate_on_create, and validate_on_update class methods. validate methods are invoked on every save operation.