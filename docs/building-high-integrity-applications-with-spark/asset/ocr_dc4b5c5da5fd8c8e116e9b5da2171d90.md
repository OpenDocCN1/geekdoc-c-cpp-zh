will always assign an in-bounds value.” For each Assert pragma the SPARK tools will generate a verification condition to check it. Likewise, the tools will use the asserted condition in the hypotheses of following verification conditions. Thus for both humans and SPARK, assertions can help clarify what is happening in the program and simplify the process of deriving conclusions about what the code does.

To illustrate some of the issues, we present a somewhat contrived example of a subprogram that calculates a student’s semester bill at a hypothetical state university. The specification of package Students provides the necessary type and subprogram declarations.

```
```ada
with Dates;
package Students
   with SPARK_Mode => On
is
   type Gender_Type is (Male, Female, Unspecified);
   type Meal_Plan_Type is (None, On_Demand, Basic, Full);
   type Student_ID is range 0 .. 999_999;
   subtype Valid_Student_ID is Student_ID range 1 .. Student_ID'Last;

   type GPA_Type is delta 0.01 range 0.00 .. 4.00;

   type Money_Type is delta 0.01 digits 7 range -99_999.99 .. +99_999.99;

   type Student_Record is private;

   -- Adjusts the tuition based on student characteristics.
   function Compute_Bill (Student : in Student_Record;
                          Base_Tuition : in Money_Type) return Money_Type
     with
       Pre => (Base_Tuition in 0.00 .. 20_000.00);

private

   type Student_Record is
      record
         Birth_Date   : Dates.Date;
         ID           : Student_ID;   -- An ID of zero means not a real student.
         Gender       : Gender_Type;
         GPA          : GPA_Type;
         Part_Time    : Boolean;
         In_State     : Boolean;      -- True if the student is a state resident.
         Resident     : Boolean;      -- True if the student resides on campus.
         Meal_Plan    : Meal_Plan_Type;
      end record;
```
```