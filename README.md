# The-Complete-PL-SQL-Bootcamp
--PL/SQL anonymous block
declare
begin
null;
end;
-- variables
declare
text1 varchar2(30) := 'hello';
numnum number(20) := 20;
numfloat number(20) := 20.20;
numpoint number(20,2) := 20.20;
numint pls_integer := 30;
numbfloat binary_float := 45.67;
date1 date := '22-MAR-18 12:01:32';
date2 timestamp := systimestamp;
date3 timestamp(6) with time zone := systimestamp;
date4 interval day(5) to second(6) := '124 04:07:23.012';
date5 interval year to month := '12-5';
begin
dbms_output.put_line(text1);
dbms_output.put_line(numnum);
dbms_output.put_line(numfloat);
dbms_output.put_line(numpoint);
dbms_output.put_line(numbfloat);
dbms_output.put_line(date1);
dbms_output.put_line(date2);
dbms_output.put_line(date3);
dbms_output.put_line(date5);
end;
--boolean data type
declare
booldata boolean := true ;
begin
  dbms_output.put_line(sys.diutil.bool_to_int(booldata));
end;
create table employees(employee_id number,employee_name varchar2(30),employee_age number,employee_mail varchar2(40))
insert into employees values (3,'asad',24,'asad@gmail.com')
-- %type attribute---------------------------------
declare
datatype1 employees.employee_id%type;
datatype2 datatype1%type;
datatype3 employees.employee_id%type;
begin
   datatype1 := 22;
   datatype2 := 23;
   datatype3 := null;
   dbms_output.put_line(datatype1);
   dbms_output.put_line(datatype2);
   dbms_output.put_line(datatype3);
end;
-- trying to assign different datatypes on %type------------------
declare
datatype1 employees.employee_id%type;
datatype2 employees.employee_name%type;
begin
   datatype1 := 'hi';
   datatype2 := 33;
   dbms_output.put_line(datatype1);
   dbms_output.put_line(datatype2);
end;
-- ORA-06502: PL/SQL: numeric or value error: character to number conversion error ORA-06512: at line 5
--ORA-06512: at "SYS.DBMS_SQL", line 1721
-- got error because we assigned  different datatypes on %type
-- delimeters and commenting ------------------
declare
 text varchar2(100) := 'pl/sql';
begin
-- this is a single comment
/*this is
a multi line 
comments */
   dbms_output.put_line(text);
end;
--pl/sql variable scope alias local variables and global variables
declare
text1 varchar2(100) := 'global variables';
text2 varchar2(100);
text3 varchar2(20);
begin
    declare
     text4 varchar2(90) := 'localvar';
    begin
     text2 := 'local variables';
     text3 := 'local';
     dbms_output.put_line(text1);	
	 dbms_output.put_line(text2);
	 dbms_output.put_line(text4);
    end;
dbms_output.put_line(text3);
dbms_output.put_line(text1);
--dbms_output.put_line(text4);
/*ORA-06550: line 17, column 22:
PLS-00201: identifier 'TEXT4' must be declared // ***** we can't call local variabl at global ******/
*/
end;
--bind variables
set serveroutput on;
set autoprint on;
/
variable var1 varchar2(100);
/
variable num1 number;
/
variable date1 date;
/
declare
var2 varchar2(100);
begin
:var1 := 'pl/sql';
:num1 := 23;
var2 := :var1;
dbms_output.put_line(:var1);
dbms_output.put_line(:num);
dbms_output.put_line(var2);
end;
--pl/sql arithmetic operators
declare
a number := 10;
b number :=2;
addition number;
subtraction number;
multiplication number;
divison number;
power number;
mod_remainder number;
begin
    dbms_output.put_line('a = '|| a || ' and ' ||'b = ' || b);
/*
    dbms_output.put_line(a || ' + ' || b  || a+b ); error because can't  add 
ORA-06502: PL/SQL: numeric or value error: character to number conversion error ORA-06512: at line 6
ORA-06512: at "SYS.DBMS_SQL", line 1721
*/
-- to solve above problem we need use logics seperately
addition := a + b;
subtraction  := a - b;
multiplication := a * b ;
divison := a / b ;
power := a ** b ;
mod_remainder := mod(a,b);
dbms_output.put_line(a || ' + ' || b  || ' = ' || addition);
dbms_output.put_line(a || ' - ' || b  || ' = ' || subtraction);
dbms_output.put_line(a || ' * ' || b  || ' = ' || multiplication);
dbms_output.put_line(a || ' / ' || b  || ' = ' || divison);
dbms_output.put_line(a || ' ** ' || b  || ' = ' || power);
dbms_output.put_line(a || ' % ' || b  || ' = ' || mod_remainder);
end;




