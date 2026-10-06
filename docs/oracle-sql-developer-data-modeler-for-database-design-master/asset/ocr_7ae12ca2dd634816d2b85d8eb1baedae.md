# Chapter 7: Generating DDL Scripts for Creating Database Objects 173

A piece of a DDL script defined as Advanced Interactive DDL for creating a table Order would look something like this:

```
...declare
  statement varchar2(32000);
  comments varchar2(200);
begin
  statement := 'PROMPT CREATING TABLE ''Order'\nCREATE TABLE ''Order'' (
  ''OrderNo'' NUMBER NOT NULL,
  ''Information'' VARCHAR2 (100 CHAR) NULL
  ORGANIZATION HEAP NOCOMPRESS NOCACHE PARALLEL NOROWDEPEPENCIES
)
disABLE ROW MOVEMENT';
comments := 'PROMPT CREATING TABLE ''Order''';
adv_scripting.EXEC_STATEMENT(10,statement,comments);
end;
/
end Step10
-- Step20
declare
  statement varchar2(32000);
  comments varchar2(200);
begin
  statement := 'COMMENT ON TABLE ''Order'' IS ''This is the table for Orders.'''
  comments := 'COMMENT ON TABLE ''Order'' ';
adv_scripting.EXEC_STATEMENT(20,statement,comments);
end;
/
end Step20
-- Step30
declare
  statement varchar2(32000);
  comments varchar2(200);
begin
  statement := 'PROMPT CREATING PRIMARY KEY ON ''Order''';
ALTER TABLE ''Order''
  ADD CONSTRAINT ''Order_PK'' PRIMARY KEY (''OrderNo'') NOT DEFERABLE
ENABLE VALIDATE '';
  comments := 'PROMPT CREATING PRIMARY KEY ON ''Order''';
ALTER TABLE ''Order''
  ADD CONSTRAIN'';
adv_scripting.EXEC_STATEMENT(30,statement,comments);
end;
/
```