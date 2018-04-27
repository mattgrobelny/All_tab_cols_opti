# All Table Column Join Optimizer
Detail out algorithm for optimizing a join of tables for a specified set of fields in a database.

# Functionality Overview
1. Import Csv of All_tab_cols for Table_name and Column_name
2. Create process storage of csv for?
  - Convert each table into a bitwise representation of each tables's fields
  - 10111011...1  where 1 is fields is in table and 0 field is not
  - Sort tables for table with most fields to least
4. Input a comma sep string of fields? autocomplete? reg ex processed?
5.
For each field:
  - Find table which represents most fields
  - Find table which represents 2nd most fields
  - Join on those tables
  - Check how many fields are still no represented
  - Find set which minimizes fields that are missing
  -
Allcols - Sampleid, site, batchno, size, num, date, plan
Sample  - Sampleid,     , batchno
Sdidata - sampleid,                           date
EMS     - sampleid,                                  plan  

sample  - 11100010
stidata - 10011110
EMS     - 10000001

Want:   - Sampleid,       batchno, size              plan           
wantbit - 1011001

1.
sample  - 11100010
want    - 10110001
keyfield- 10100000 # all fields which are key
--------------------
Same    - 10100000
--------------------
Dif_want- 00010001
want = Dif_want

1st tb - sample
join on 10100001

## continue checker?

2.
Sdidata - 10011110 # should have most over lapping fields in want
want    - 00010001
keyfield- 10100000 # want must have at least 1 in key field
--------------------
Same    - 00010000
--------------------
Dif_want- 00000001
want = Dif_want

2nd tb - sdidata
join on 00010001  

3.
EMS     - 10011110
want    - 10000001
keyfield- 10100000 # want must have at least 1 in key field
--------------------
Same    - 00010001
--------------------
Dif_want- 00010001

3rd tb - EMS
join on 00010001  

## Final Check
sample  - 11100010
stidata - 10011110
EMS     - 10011110
--------------------
Sum     - 11111111
wantbit - 10110011
--------------------
Sum&Wntb- 10110011  # needs to eql wantbit

## confirm each 
