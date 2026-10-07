
# Introduction to Databases

| course | faculty | faculty id | faculty name | office |
|---|---|---|---|---|---|
| CSC-132A | Introduction to Programming | J33486 | A52990 | Black Anderson | MTC-218 |
| CSC-132B | Introduction to Programming | B78880 | A77587 | Debbie Angle | MTC-320 |
| CSC-230 | Algorithms & Structures | A77587 | B66750 | Alice Brown | MTC-257 |
| CSC-232A | Programming | B66750 | B78880 | Ying Bai | MTC-211 |
| CSC-232B | Programming | A77587 | B86590 | Davalla Mathis | MTC-214 |
| CSC-233A | Introduction to Algorithms | H99118 | H99118 | Jeff Henry | MTC-336 |
| CSC-233B | Introduction to Algorithms | K69880 | J33486 | Steve John | MTC-118 |
| CSC-234A | Data Structure & Algorithms | B78880 | K69880 | Jenny King | MTC-324 |

FIGURE 2.8 Course (partial data shown) Faculty (partial data shown).

## 2.5 DEFINE RELATIONSHIPS

### 2.5.1 CONNECTIVITY

Connectivity refers to the types of relationships that entities can have. Basically, this can be one-to-one, one-to-many, and many-to-many. In ER diagrams these are indicated by placing 1, M or N at one of the ends of the relationship diagram. Figures 2.9–2.12 use the illustration of this notation.

- **A one-to-one (1:1)** relationship occurs when one instance of entity A is related to one instance of entity B. For example, user_name in the Login table and user_name in the Student table (Figure 2.9).
- **A one-to-many (1:M)** relationship occurs when one instance of entity A is associated with zero or many instances of entity B. However, department can have many faculty members; each faculty member is assigned to only one department. In CSEDEPT database, a one-to-many relationship is represented by faculty_id in the Faculty table and faculty_id in the Student and Course table (Figure 2.10).
- **A many-to-many (M:N)** relationship occurs when one instance of entity A is associated with zero or many instances of entity B. For example, a student may take many courses and one course may be taken by more than one, as shown in Figure 2.11. In CSEDEPT database, a many-to-many relationship can be realized using the third table between the Student and Course tables.

| user_name | user_name | gpa | credits | student_id |
|---|---|---|---|---|
| ajade | ajade | 3.26 | 18 | A97850 |
| awoods | awoods | 3.57 | 16 | A78835 |
| bvalley | bvalley | 3.52 | 10 | B92996 |
| hsmith | hsmith | 3.87 | 78 | H10210 |
| terica | terica | 3.95 | 12 | J77896 |

FIGURE 2.9 One-to-one relationship in the Login and Student tables.

| faculty id | faculty name | office |
|---|---|---|
| A52990 | Andrew | MTC-218 |
| A75587 | Debby Angle | MTC-320 |
| B96750 | Alice Brown | MTC-257 |
| B78680 | Ying Bai | MTC-211 |
| B86590 | David | MTC-214 |
| H99118 | Jeff Henry | MTC-336 |
| J33486 | Steve Johnson | MTC-118 |
| K69880 | Jenny King | MTC-324 |

| course id | course | faculty id |
|---|---|---|
| CSC-132A | Introduction to Programming | J33486 |
| CSC-132B | Introduction to Programming | B78880 |
| CSC-230 | Algorithms & Structures | A77587 |
| CSC-232A | Programming I | B66750 |
| CSC-232B | Programming I | A77587 |
| CSC-233A | Introduction to Algorithms | H99118 |
| CSC-234A | Data Structure & Algorithms | B78880 |

FIGURE 2.10 One-to-many relationship between faculty and course.

| student id | student name | gpa | credits |
|---|---|---|---|
| A78853 | Andrew Woods | 3.26 | 108 |
| A97850 | Ashley Jade | 3.57 | 116 |
| B92996 | Blue Valley | 3.52 | 102 |
| H10210 | Holes Smith | 3.87 | 78 |
| T77896 | Tom Erica | 3.95 | 127 |

| course id | course | faculty id |
|---|---|---|
| CSC-132A | Introduction to Programming | J33486 |
| CSC-132B | Introduction to Programming | B78880 |
| CSC-230 | Algorithms & Structures | A77587 |
| CSC-232A | Programming I | B66750 |
| CSC-233B | Programming I | A77587 |
| CSC-233A | Introduction to Algorithms | H99118 |

## StudentCourse

| s_course id | student id | course id | credit |
|---|---|---|---|
| 1000 | H10210 | CSC-131D | 3 CE |
| 1001 | B92996 | CSC-132A | 3 CS/IS |
| 1002 | T77896 | CSC-335 | 3 CS/IS |
| 1003 | A78835 | CSC-331 | 3 CE |
| 1004 | H10210 | CSC-234B | 3 CE |
| 1005 | T77896 | CSC-233A | 3 CS |
| 1006 | B92996 | CSC-233A | 3 CS/IS |

FIGURE 2.11 Many-to-many relationship between student and course tables.

This database design assumes that the course table only contains courses taught by all faculty members in this department for one semester. Therefore, each course can only be taught by a unique faculty. If one wants to develop a Course table contains courses taught by all faculty in more than one semester, the third table, say FacultyCourse, should be created to set up a many-to-many relationship between the Faculty and the Course table since one course may be taught by different faculty for the different semester.

The relationships in CSEDEPT database are summarized in Figure 2.12.

Database name: CSE_DEPT

The five entities are:

- Login
- Faculty
- Course
- Student
- StudentCourse

![](img/d59a47501d0a20fc0460a49c6fb7_47_0)
FIGURE 2.12 Relationships in CSEDEPT database.

## Introduction to Databases

19

![](img/d59a47501d0a20fc0460a49c6fb7_47_1)
FIGURE 2.13 Relationships are illustrated using MS Access.

## SQL Server Programming with C

Entity is represented by a rectangular box.

![](img/d59a47501d0a20fc0460a49c6fb7_48_0)

A weak entity is represented by a double rectangular box.

![](img/d59a47501d0a20fc0460a49c6fb7_48_1)

An attribute is represented by an oval.

![](img/d59a47501d0a20fc0460a49c6fb7_48_2)

Relationship is represented by a diamond with lines connecting the entities.

![](img/d59a47501d0a20fc0460a49c6fb7_48_3)

Cardinality is indicated by placing 1, N, or M near the entity it is associated with.

| 1 | M |

A line links entities to attributes.

![](img/d59a47501d0a20fc0460a49c6fb7_48_4)

FIGURE 2.14 Commonly used symbols for ER notation.

## 2.6 ER NOTATION

There are a number of ER notations available, including Chen’s, Bachman, Crow’s foot and a few others. There is at present no consensus on the symbols and the styles used to draw ERDs. A number of drawing tools are available to draw ERDs. These include ER Assistant, Microsoft Visio, and Smart Draw, many others. The commonly used notations are shown in Figure 2.14.

## 2.7 DATA NORMALIZATION

After identifying tables, attributes, and relations the next logical step in database design is to make sure that the database structure is optimal. The optimum structure is achieved by eliminating redundancies, unnecessary inefficiencies, and deletion anomalies that usually occur in normalized or partially normalized databases. Data normalization is a progressive process. The steps in the normalization process are called normal forms. Each normal form progressively improves the database and makes it more efficient. In other words, a database that is in second normal form is better than the one in the first normal form, and one in third normal form is better than in second normal form. To be in the third normal form a database has to be in both the first and second normal
