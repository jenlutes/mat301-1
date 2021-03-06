
### Data design

---
 

Consider the design of a data structure.  It is important to have a well-designed database to make queries easy and to advoid redundant data.  Steps in the design of a data structure are:

1. __Identify data elements__ (make a list.  For example, customer's name would be a data element of an order)
2. __Subdivide elements into smallest useful component__ (address can be split into 4 or 5 parts including city, state, and zip)
3. __Identify tables and assign columns__ (group elements into "entities" = tables)
4. __Identify primary and foreign keys__.  Each table needs a primary key.  There are different schools of thought, take notice.  If for each element in one table there exists several related elements in another table, include a foreign key in the "many" table. (Also see __Referential integrity__)
5. Normalize
6. Identify indexes


##### Referential Integrity
Referential integrity preserves relationships between tables so as to not create _orphaned_ rows.  Referential integrity (if you want to have it) must be declaired using foreign key constraints.  For example, if a row in the primate key table is deleted, then what happens to the related rows in the foreign key table?  Similar circumstances can occur if inserting a row in foreign key table, or updating values in either table.

##### Normalization


__Normalization__ is the process of splitting a relation with more than one theme into a set of (related) relations each having only one theme.  Normalization eliminates data redundancy (which causes storage and maintenance problems).  Normalization must be applied in sequential order.  There are 7 forms, but in practice typically only 3 are used.  In some cases you __denormalize__ a data structure. We cover the first three.

1. (1NF) All data is atomic (indivisible units).  More specifically, rows contain data about one entity (e.g., products), no two rows hold identical data, and no repeated columns.  Primary key is set and all attributes depend on primary key.

2. (2NF) Split any partial depended data into separate table.  For example, if customer table contained order information (as customers place orders), move order data to new table.  To apply, data must already be in 1NF.  

3. (3NF)  Non-key columns must depend _only_ on primary key, that is remove transitive dependencies.  Order lines (specific items and quantities) are not solely dependent on order_id, as other customers can order the same products.   Another example, employee position information is not dependent on the employee.  More specifically, "associate professor" and the duties/description of the position are not dependent on me.  To apply, data must already be in 2NF.

Example:


| __Proj #__ | __Proj. Name__ | __Emp #__ | __Emp Name__  | __Job__              | __Rate__ | __Hours__ |
|------------|----------------|-----------|---------------|----------------------|----------|-----------|
| 15         | Evergreen      | 103       | Mary Jane     | Ele. Engineer        | 85.50    | 23.8      |
|            |                | 101       | John Newhall  | DBA                  | 105.00   | 19.4      |
|            |                | 105       | Alice Johnson | Programmer           | 45.75    | 12.8      |
|            |                | 102       | David Silver  | System Analyst       | 96.50    | 21.4      |
| 17         | Tinkers Creek  | 114       | James Frommer | Clerical Support     | 26.89    | 48.8      |
|            |                | 103       | Mary Jane     | Ele. Engineer        | 85.50    | 19.7      |
|            |                | 118       | Ann Ramorous  | System Analyst       | 96.50    | 34.2      |
|            |                | 123       | Larry Ludwig  | Application Designer | 48.10    | 58.2      |
|            |                | 124       | Ralph DeMouth | General Support      | 18.36    | 14.1      |
| 20         | Caller 9       | 102       | David Silver  | System Analyst       | 96.50    | 12.0      |
|            |                | 101       | John Newhall  | DBA                  | 105.00   | 37.5      |
|            |                | 111       | James Frommer | Clerical Support     | 26.89    | 39.5      |
