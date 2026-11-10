```
```text
R_SALV_TREE = lo_tree
CHANGING
  t_table = it_outtab.

* Add the nodes to the tree
NODES = lo_tree->get_nodes( ).
LOOP AT it_sflight INTO wa_sflight.
  ON CHANGE OF wa_sflight-carrid.
    CLEAR key.
    TRY.
      node = nodes->add_node( related_node = KEY
        relationship = cl_gui_column_tree=>relat_first_child
        data_row = wa_sflight ).
      KEY = node->get_key( ).
    CATCH cx_salv_msg.
    ENDTRY.
  ENDON.
  TRY.
    node = nodes->add_node( related_node = KEY
      relationship = cl_gui_column_tree=>relat_last_child
      data_row = wa_sflight ).
  CATCH cx_salv_msg.
  ENDTRY.
ENDLOOP.
columns = lo_tree->get_columns( ).
columns->set_optimize( abap_true ).
*Set default status
lo_functions = lo_tree->get_functions( ).
lo_functions->set_all( abap_true ).
*Display table
lo_tree->display( ).
```
```

# Listing 15.17 Tree Display

In Listing 15.17, we're selecting data from table SFLIGHT and displaying it as a tree structure. We've defined an internal table IT_OUTTAB, which is of the same type as the internal table IT_SFLIGHT.

The empty table IT_OUTTAB is passed to the factory method, and the reference to the tree object is assigned to the LO_TREE reference object. We're getting the nodes references via the GET_NODES method. The records are added to the tree structure by looping the internal table IT_SFLIGHT and calling the ADD_NODE method of the nodes object. To this method, the record of the internal table and the node relationship is transferred, which is displayed as a node in the output.