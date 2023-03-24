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
--pl/sql if else conditions
-- numbers
declare
a number := 3;
b number := 2;
begin
    if a < b then
    dbms_output.put_line(a || ' < ' || b);
	elsif a > b then
    dbms_output.put_line(a || ' > ' || b);
	else 
    dbms_output.put_line(a || ' =' || b);
	end if;
end;
-- text/ strings
declare
text varchar2(30) := 'hi';
text1 varchar2(30) := 'HI';
begin
    if text = 'hi' then
    dbms_output.put_line(text);
	elsif text1 = 'HI' then
    dbms_output.put_line(text1);
	else 
    dbms_output.put_line('not matching/found');
	end if;
end;
-- in condition statements pl/sql is case sensitive // same format as assigned variable 
--pl/sql case --------------------------------
declare
day_name varchar2(100) := 'THU';
begin
	case day_name 
        when 'SUN' then dbms_output.put_line('SUNDAY');
		when 'MON' then dbms_output.put_line('MONDAY');
    	when 'TUE' then dbms_output.put_line('TUESDAY');
    	when 'WED' then dbms_output.put_line('WEDNESDAY');
    	when 'THU' then dbms_output.put_line('THURSDAY');
    	when 'FRI' then dbms_output.put_line('FRIDAY');
        when 'SAT' then dbms_output.put_line('SATURDAY');
	ELSE
        dbms_output.put_line('NOT A DAY');
    end case;
end;
--pl/sql loops
-- basic loop
declare
a number := 0;
begin
    loop
    dbms_output.put_line(a);
    a := a + 1;
    exit when a > 10;
    end loop;
end;
-- for loop
declare
a number := 0;
begin
    for a in 0..10 loop
    dbms_output.put_line(a);
    end loop;
end;
-- while loop
declare
a number := 0;
begin
    while a < 11 loop
    dbms_output.put_line(a);
    a := a + 1;
-- exit when a >11;
    end loop;
end;
-- for loop
declare
a number := 0;
begin
    for b in 0..10 loop
    dbms_output.put_line(b);
    end loop;
end;
-- basic loop
declare
a number := 0;
begin
    loop
    dbms_output.put_line(a);
    a := a + 1;
    if  a > 10 then
    exit;
	end if;
    end loop;
end;
-- nested loops
declare
 a number := 0;
begin
    for b in 0..8 loop
        dbms_output.put_line('outer := ' || b);
		 a :=1;
		loop
            a := a + 1;
			dbms_output.put_line('inner := ' || a);
            exit when a > 5;
        end loop;
    end loop;
end;
-- nested loops with labels
declare
 a number := 0;
begin
<<outer_loop>>
    for b in 0..8 loop
        dbms_output.put_line('outer := ' || b);
		 a :=1;
		<<inner_loop>>
		loop
            a := a +1;
			dbms_output.put_line('inner := ' || a);
            exit when a > 5;
        end loop inner_loop;
    end loop outer_loop ;
end;
-- continue statement 
declare
 a number := 0;
begin
    for b in 0..8 loop
        dbms_output.put_line('outer := ' || b);
		 a :=1;
		loop
            a := a + 1;
			dbms_output.put_line('inner := ' || a);
			continue when a = 3;
            exit when a > 5;
        end loop;
    end loop;
end;
--inner loop
declare
a number := 0;
begin
    for a in 0..10 loop
    dbms_output.put_line(a);
    continue when a = 3; -- skip the 3 number
    end loop;
end;
-- go to statement
declare
searching number :=2;
is_prime  boolean := true;
begin
 for a in 2..searching -1 loop
   if mod(is_prime,a) = 0 then
      dbms_output.put_line(searching || 'is not a prime number');
	  is_prime := false;
	  goto end_point;
   end if;
  end loop;
 if is_prime then
  dbms_output.put_line(searching || 'is  a prime number');
 end if;
<<end_point>>
   dbms_output.put_line('checked successfully');
end;
-- table
create table employees(employee_id number primary key,employee_name varchar2(100),employee_age number,employee_email varchar2(100)) 
insert into employees values (1,'abc',22,'abc@gmail.com')
insert into employees values (2,'bcd',23,'bcd@gmail.com')
insert into employees values (3,'cgh',24,'cgh@gmail.com')
insert into employees values (4,'tyh',25,'tyh@gmail.com')
insert into employees values (5,'jkl',25,'jkl@gmail.com')
-- selected queries
declare
 p_name varchar2(100);
 p_emp_id employees.employee_id%type;
begin
  --select employee_name,employee_id into p_name,p_emp_id from employees;
  select employee_name,employee_id into p_name,p_emp_id from employees where employee_id = 2;
  dbms_output.put_line(p_name);
  dbms_output.put_line(p_emp_id);
end;
--dml queries
declare
 p_name varchar2(100);
 p_emp_age employees.employee_age%type;
begin
  for i in 6..9 loop
    /*insert into employees (employee_id,employee_name,employee_age,employee_email) values
    (i,'ghjdf',30,'ghjdf@gmail.com');*/
    --update employees set employee_age =  employee_age +1 where employee_id = 2;
    --delete from employees where employee_id = 2;
-- we can use all above dml commands they all works
   end loop;
end;
-- sequence
create sequence s_emp_id start with 6 increment by 1;
begin
for i in 6..9 loop
    insert into employees (employee_id.nextval,employee_name,employee_age,employee_email) values
    (i,'ghjdf',30,'ghjdf@gmail.com');
end loop;
end;




