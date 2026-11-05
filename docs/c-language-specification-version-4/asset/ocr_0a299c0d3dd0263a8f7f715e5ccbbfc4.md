variable-declarator:
    identifier
    identifier = variable-initializer
variable-initializer:
    expression
    array-initializer
method-declaration:
    method-header method-body
method-header:
    attributes_opt method-modifiers_opt partial_opt return-type member-name type-parameter-list_opt
        ( formal-parameter-list_opt ) type-parameter-constraints-clauses_opt
method-modifiers:
    method-modifier
    method-modifiers method-modifier
method-modifier:
    new
    public
    protected
    internal
    private
    static
    virtual
    sealed
    override
    abstract
    extern
return-type:
    type
    void
member-name:
    identifier
    interface-type . identifier
method-body:
    block
    ;
formal-parameter-list:
    fixed-parameters
    fixed-parameters , parameter-array
    parameter-array
fixed-parameters:
    fixed-parameter
    fixed-parameters , fixed-parameter
fixed-parameter:
    attributes_opt parameter-modifier_opt type identifier default-argument_opt
default-argument:
    = expression