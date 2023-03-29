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
create table employees(employee_id number primary key,employee_name varchar2(100),employee_age number ,employee_email varchar2(100))
insert into employees values (3,'bcud',25,'bcud@gmail.com')
create table employees1(employee_id number primary key,pr_name varchar2(100),employee_exp number ,project_email varchar2(100))
insert into employees1 values (2,'lomq',2,'lomq@gmail.com')
declare
p_name employees.employee_name%type;
begin
    select employee_name into p_name from employees where employee_id =1;
    dbms_output.put_line(p_name);
end;
--pl/sql records
-- record is similar as selecting a single row
declare
record_employee employees%rowtype;
begin
  select * into record_employee from employees where employee_id =1;
    dbms_output.put_line(' id :-'||record_employee.employee_id || ', name is '||record_employee.employee_name || ', has age ' ||record_employee.employee_age|| ', and mail is :-'|| record_employee.employee_email );  
end;
-- creating record
declare
type type_emp is record (employee_id number,employee_name varchar2(100),employee_age number ,employee_email varchar2(100));
RECORD_EMPLOYEE TYPE_EMP;
begin
record_employee.employee_id := 6;
record_employee.employee_name := 'klq';
record_employee.employee_age := 29;
record_employee.employee_email := 'klq@gmail.com';
  --select * into type_emp from employees where employee_id =1;
    dbms_output.put_line(' id :-'||record_employee.employee_id || ', name is '||record_employee.employee_name || ', has age ' ||record_employee.employee_age|| ', and mail is :-'|| record_employee.employee_email );  
end;
---
declare
type type_emp is record (employee_id number,employee_name varchar2(100),employee_age number ,employee_email varchar2(100));
test_employee type_emp;
begin
test_employee.employee_id := 7;
test_employee.employee_name := 'king';
test_employee.employee_age := 30;
test_employee.employee_email := 'king@gmail.com';
  --select * into type_emp from employees where employee_id =1;
    dbms_output.put_line(' id :-'||test_employee.employee_id || ', name is '||test_employee.employee_name || ', has age ' ||test_employee.employee_age|| ', and mail is :-'|| test_employee.employee_email );  
end;
-- select statement
declare
type type_emp is record (employee_id number,employee_name varchar2(100),employee_age number ,employee_email varchar2(100));
RECORD_EMPLOYEE TYPE_EMP;
begin
  select * into RECORD_EMPLOYEE from employees where employee_id =1;
    dbms_output.put_line(' id :-'||record_employee.employee_id || ', name is '||record_employee.employee_name || ', has age ' ||record_employee.employee_age|| ', and mail is :-'|| record_employee.employee_email );  
end;
-- we can also insert multiple tables at a time
declare
type type_emp1 is record (employee_id number,employee_name varchar2(100),employee_age number ,employee_email varchar2(100));
type type_emp2 is record (employee_id number,pr_name varchar2(100),employee_exp number ,project_email varchar2(100));
RECORD_EMPLOYEE type_emp1;
begin
     select * into RECORD_EMPLOYEE from employees where employee_id =1;
RECORD_EMPLOYEE.project.employee_id := 1;
RECORD_EMPLOYEE.project_name := 'king';
RECORD_EMPLOYEE.employee_exp := 3;
RECORD_EMPLOYEE.project_email := 'king@gmail.com';
    dbms_output.put_line(' id :-'||record_employee.employee_id || ', name is '||record_employee.employee_name || ', has age ' ||record_employee.employee_age|| ', and mail is :-'|| record_employee.employee_email );  
    dbms_output.put_line(' id :-'||RECORD_EMPLOYEE.project.employee_id || ', name is '||RECORD_EMPLOYEE.project_name || ', has age ' ||RECORD_EMPLOYEE.employee_exp || ', and mail is :-'|| RECORD_EMPLOYEE.project_email );  
end;
--dml commands - record  
create table employees3 as select * from employees where 1=2;
select * from employees3;
declare
 record_employee employees%rowtype;
begin
   select * into record_employee from employees where employee_id = 2;
   insert into employees3 values record_employee;
end;
-- varray alias arrays in programing languages
declare
 type va_list is varray(6) of varchar2(10);
 employees va_list;
begin
/* varray(6) 6 size and inside (va_list) elements must same number
    array starts index at 1 not 0 like in python */
  employees := va_list('abc','bcd','qwe','iop','apg','laq');
  for k in 1..6 loop
   dbms_output.put_line(employees(k));
  end loop;
end;
-- using count function
declare
 type va_list is varray(6) of varchar2(10);
 employees va_list;
begin
/* varray(6) 6 size and inside (va_list) elements must same number
    array starts index at 1 not 0 like in python */
  employees := va_list('abc','bcd','qwe','iop','apg','laq');
  for k in 1..employees.count() loop
   dbms_output.put_line(employees(k));
  end loop;
end;
-- we can write as required elements in an varray
declare
 type va_list is varray(100) of varchar2(10);
 employees va_list;
begin
/* varray(6) 6 size and inside (va_list) elements must same number
    array starts index at 1 not 0 like in python */
  employees := va_list('aqbc','bcqd','qweq','ioqp','adpg','lahq','hbcgfej');
  for k in 1..employees.count() loop
   dbms_output.put_line(employees(k));
  end loop;
end;
--using first and last function
declare
 type va_list is varray(100) of varchar2(10);
 employees va_list;
begin
/* varray(6) 6 size and inside (va_list) elements must same number
    array starts index at 1 not 0 like in python */
  employees := va_list('aqbc','bcqd','qweq','ioqp','adpg','lahq','hbcgfej','cdshjs');
  for k in employees.first()..employees.last() loop
   dbms_output.put_line(employees(k));
  end loop;
end;
-- if exists
declare
 type va_list is varray(100) of varchar2(10);
 employees va_list;
begin
  employees := va_list('aqbc','bcqd','qweq','ioqp','adpg','lahq','hbcgfej','cdshjs');
  for k in 1..8 loop
    -- for range must be the start and end index number of array not exceeded.
    if employees.exists(k) then
     dbms_output.put_line(employees(k));
    end if;
end loop;
end;
--retrieving from tables
create table employees (employee_id number,employee_name varchar2(10),employee_age number ,employee_mail varchar2(100))
insert into employees values (2,'kat',24,'kat@gmail.com')
select * from employees;
declare
  type va_list is varray(100) of varchar2(10);
  employees va_list:= va_list();
  idx number :=1;
begin
    for k in 1..5 loop
    employees.extend;
    select employee_name into employees(idx) from employees where employee_id =1;
    idx := idx +1;
    dbms_output.put_line(employees(k));
    end loop;
end;
-- nested tables
/* similar as varrays
 have key value pairs
max 2 gb 
delete and not stored consecutevely
nested tables are not bounded
*/
declare
 type p_list is table of varchar2(50);
 emp p_list;
begin
  emp := p_list('abn','djjd','hjdsj','jsjs');
   for k in 1..4 loop
   dbms_output.put_line(emp(k));
   end loop;
end;
-- appending elements
declare
 type p_list is table of varchar2(50);
 emp p_list;
begin
  emp := p_list('abn','djjd','hjdsj','jsjs');
   emp.extend;
   emp(5) := 'fjsdko';
   for k in 1..4 loop
   dbms_output.put_line(emp(k));
   end loop;
end;
--pl/sql associative arrays
create table employees(emp_id number,emp_name varchar2(100))
insert into employees values (5,'nmkpk')
select * from employees;
alter table employees add phn_no1 number;
declare
type aa_list is table of employees%rowtype index by employees.emp_name%type;
emplos aa_list;
id employees.emp_id%type;
n_name employees.emp_name%type;
begin
    for k in 1..3 loop
    select * into emplos(k) from employees where emp_id =1;
    end loop;
 id := emplos.first;
    while id is not null loop
        dbms_output.put_line(emplos(id).emp_name);
    id := emplos.next(id);
    end loop;
end;
----delete 
declare
type aa_list is table of employees%rowtype index by employees.emp_name%type;
emplos aa_list;
id employees.emp_id%type;
n_name employees.emp_name%type;
begin
    for k in 1..5 loop
    select * into emplos(k) from employees where emp_id =1;
    end loop;
    emplos.delete(3,4);
 id := emplos.first;
    while id is not null loop
        dbms_output.put_line(emplos(id).emp_name);
    id := emplos.next(id);
    end loop;
end;
--reverse 
declare
type aa_list is table of employees%rowtype index by employees.emp_name%type;
emplos aa_list;
id employees.emp_id%type;
n_name employees.emp_name%type;
begin
    for k in 1..5 loop
    select * into emplos(k) from employees where emp_id =1;
    end loop;
 id := emplos.first;
    while id is not null loop
        dbms_output.put_line(emplos(id).emp_name);
    id := emplos.prior(id);
-- prior prints last to first
    end loop;
end;
-- for loop reverse *************************
declare
a number := 10;
begin
   for a in 10..1 loop
     dbms_output.put_line(a);
   end loop;
end;
-- ******************************************
--storing collections
create or replace type phn_no as object (ph_type varchar2(10),ph_number number)
create or replace type phn_no1 as varray(5) of phn_no;
insert into employees values (5,'yuu',phn_no1(phn_no('lan',123),phn_no1(phn_no('pho',1223)));
-- nested table
create table employees1(emp_id number,emp_name varchar2(100),phn_num number) nested table phn_num store as phn_num_table;
insert into employees1 values (5,'yuu',phn_no1(phn_no('lan',123),phn_no1(phn_no('pho',1223)));
--pl/sql cursors
create  table employees (emp_id number,emp_name varchar2(30),emp_age number,emp_mail varchar2(20))
insert into employees values (3,'iai',24,'iai@gmail.com')
-- implicit curosrs are automatic alias inbuilt functions
-- explicit cursors are user defined
-- explicit cursor example
declare
  cursor emp is select emp_name,emp_mail from employees;
/* in select statement we need to select the required columns and must be same number of we declaring
*/
  name employees.emp_name%type;
  mail employees.emp_mail%type;
begin
  open emp;
-- we can fetch the all the rows in a table one by one
  fetch emp into name,mail;
  dbms_output.put_line(name || ' '|| mail);
  fetch emp into name,mail;
  dbms_output.put_line(name || ' '|| mail);
  fetch emp into name,mail;
  dbms_output.put_line(name || ' '|| mail);
  close emp;
end;
-- cursors with record
declare
  type rec_emp is record (name employees.emp_name%type,mail employees.emp_mail%type);
  cursor emp is select emp_name,emp_mail from employees;
/* in select statement we need to select the required columns and must be same number of we declaring
*/
  va_emp rec_emp;
begin
  open emp;
-- we can fetch the all the rows in a table one by one
  fetch emp into va_emp;
  dbms_output.put_line(va_emp.name || ' '|| va_emp.mail);
  fetch emp into va_emp;
  dbms_output.put_line(va_emp.name || ' '|| va_emp.mail);
  fetch emp into va_emp;
  dbms_output.put_line(va_emp.name || ' '|| va_emp.mail);
  close emp;
end;
-- cursor loops
declare
  cursor emp is select * from employees where emp_id =1;
/* in select statement we need to select the required columns and must be same number of we declaring
*/
  va_emp emp%rowtype;
begin
  open emp;
  loop
-- we can fetch the all the rows in a table one by one
   fetch emp into va_emp;
   dbms_output.put_line( va_emp.emp_id|| ' '|| va_emp.emp_mail);
   end loop;
   close emp;
end;
--loop to get unique data for above we get same data
declare
  cursor emp is select * from employees where emp_id =1;
  va_emp emp%rowtype;
begin
  open emp;
  loop
   fetch emp into va_emp;
   exit when emp%notfound;
   dbms_output.put_line( va_emp.emp_id|| ' '|| va_emp.emp_mail);
   end loop;
   close emp;
end;
-- while loop
declare
  cursor emp is select * from employees where emp_id =1;
  va_emp emp%rowtype;
begin
   open emp;
   fetch emp into va_emp;
   while emp%found loop
   dbms_output.put_line( va_emp.emp_id|| ' '|| va_emp.emp_mail);
   fetch emp into va_emp;
   end loop;
   close emp;
end;
-- for loop
declare
  cursor emp is select * from employees where emp_id =1;
  va_emp emp%rowtype;
begin
   open emp;
   for k in 1..3 loop
   fetch emp into va_emp;
   dbms_output.put_line( va_emp.emp_id|| ' '|| va_emp.emp_mail);
   end loop;
   close emp;
end;
--loop to get unique data for above we get same data
declare
  cursor emp is select * from employees where emp_id =1;
  va_emp emp%rowtype;
begin
  open emp;
  loop
   fetch emp into va_emp;
   exit when emp%notfound;
   dbms_output.put_line( va_emp.emp_id|| ' '|| va_emp.emp_mail);
   end loop;
   close emp;
end;
-- while loop
declare
  cursor emp is select * from employees where emp_id =1;
  va_emp emp%rowtype;
begin
   open emp;
   fetch emp into va_emp;
   while emp%found loop
   dbms_output.put_line( va_emp.emp_id|| ' '|| va_emp.emp_mail);
   fetch emp into va_emp;
   end loop;
   close emp;
end;
-- for loop
declare
  cursor emp is select * from employees where emp_id =1;
  va_emp emp%rowtype;
begin
   open emp;
   for k in 1..3 loop
   fetch emp into va_emp;
   dbms_output.put_line( va_emp.emp_id|| ' '|| va_emp.emp_mail);
   end loop;
   close emp;
end;
--cursors with parameters
create table employees (emp_id number);
insert into employees values (1);
declare
  cursor para (p_id number) is select emp_id from employees;
  va_emp para%rowtype;
begin
  open para(10);
  fetch para into va_emp;
  dbms_output.put_line(va_emp.emp_id);
  close para;
end;
-- loop 
declare
  cursor para (p_id number) is select emp_id from employees;
  va_emp para%rowtype;
begin
  open para(10);
  fetch para into va_emp;
  dbms_output.put_line(va_emp.emp_id);
  close para;
  open para(10);
  loop
  fetch para into va_emp;
  exit when para%notfound;
  dbms_output.put_line(va_emp.emp_id);
  end loop;
  close para;
end;
-- cursor attributes
-- %found , %notfound , % isopen %rowcount
declare
  cursor att is select * from employees;
  var_emp att%rowtype;
begin
 if not att%isopen then
   open att;
   dbms_output.put_line('pl/sql');
 end if;
   dbms_output.put_line(att%rowcount);
   fetch att into var_emp;
   dbms_output.put_line(att%rowcount);
   fetch att into var_emp;
   dbms_output.put_line(att%rowcount);
   close att;
   open att;
    loop
     fetch att into var_emp;
      exit when att%notfound;
        dbms_output.put_line(att%rowcount);
      end loop;
      close att;
end;
-- for update cursors
-- for update is locking and granting users
create table employees (emp_id number,emp_name varchar2(28));
insert into employees values(1,'qos');
-- we need to create another user
create user abc identified by 12;
grant create session to abc;
grant select any table to abc;
grant update on [database_name].employees to abc;
update [database_name].employees  set emp_name ='naj' where emp_id = 1;
declare
 cursor uc is select * from employees;
begin
  for r in uc in loop
    update employees set emp_name = 'naj' where emp_id = 1;
   end loop;
end;
select * from employees;
--where current clause
select * from employees
declare
 cursor cc is select * from employees;
begin
 for r_emp in cc loop
   update employees set emp_name = 'naj' where emp_id = r_emp.emp_id;
 end loop;
end;
-- reference cursors
-- reference cursors like pointers store memory address of variables
declare
 type te_emp is ref cursor return employees%rowtype;
 rc_emp te_emp;
 rr_emp  employees%rowtype;
begin
 open rc_emp for select * from employees;
 loop
 fetch rc_emp into rr_emp;
 exit when rc_emp%notfound;
 dbms_output.put_line(rr_emp.emp_id);
 end loop;
 close cursor;
end;
create table employees (emp_id number,emp_name varchar2(10))
insert into employees values (2,'abc')
alter table employees add emp_loc varchar2(20);
insert into employees (emp_loc) values ('blr');
update employees set emp_sal = 20000 where emp_id = 2;
alter table employees add emp_sal number;
select * from employees
--pl/sql exceptions
declare
name varchar2(100);
begin
select emp_name into name from employees where emp_id =2;

dbms_output.put_line(name);
exception
  when no_data_found then
     dbms_output.put_line('with that employee_id there is no data');
end;
-------
declare
name varchar2(100);
begin
select emp_name into name from employees where emp_name = 'abc';
dbms_output.put_line(name);
exception
  when no_data_found then
     dbms_output.put_line('with that employee_id there is no data');
  when too_many_rows then
     dbms_output.put_line('The name :- ' || name  || ' is same for more than one employee');
end;
-- if other errors
declare
name varchar2(100);
loca varchar2(1);
begin
--select emp_name into name from employees where emp_name = 'abc';
select emp_loc into loca from employees where emp_id = 1;
     --dbms_output.put_line(name);
     dbms_output.put_line(loca);
exception
  when no_data_found then
     dbms_output.put_line('with that employee_id there is no data');
  --when too_many_rows then
     --dbms_output.put_line('The name :- ' || name  || ' is same for more than one employee');
  when others then
     dbms_output.put_line('an unexpected error occured');
     dbms_output.put_line(sqlcode || sqlerrm);
end;
--non predefined exceptions
declare
   cannot_update_to_null exception;
   pragma exception_init(cannot_update_to_null,-01407);
begin
  update employees set emp_loc = null where emp_id = 2;
exception
  when cannot_update_to_null then
    dbms_output.put_line('we cant update a null value');
end;
-- used defined exceptions
declare
 high_sal exception;
 e_sal pls_integer;
begin
 select emp_sal into e_sal from employees where emp_id =2;
 if e_sal > 10000 then
  raise high_sal;
 end if;
 dbms_output.put_line('salary is high');
exception
    when high_sal then
     dbms_output.put_line('salary is high');
end;
-- raise__application_error
declare
 high_sal exception;
 e_sal pls_integer;
begin
 select emp_sal into e_sal from employees where emp_id =2;
 if e_sal > 10000 then
  raise high_sal;
 end if;
 dbms_output.put_line('salary is high');
exception
    when high_sal then
     dbms_output.put_line('salary is high');
    raise_application_error(-202453,'salary is high',true);
end;
-- pl/sql procedure
-- asssigning values in  declare 
-- in is input and out is output
create or replace procedure addi(a in number,b in number,c out number)
is
begin
c := a + b;
end addi;
declare
a number :=1;
b number :=2;
c number;
begin
  addi(a,b,c);
  dbms_output.put_line(' sum of ' || a || ' and ' || b || ' = '|| c);
  dbms_output.put_line(a || ' + ' || b || ' = '|| c);
end;
-- assigning values in procedure
declare
a number;
b number;
c number;
begin
  addi(4,5,c);
  dbms_output.put_line('sum of numbers is ' || c );
  dbms_output.put_line(' sum of ' || a || ' and ' || b || ' = '|| c); -- not printing a and b values 
end;
-- sub 
create or replace procedure subr(a in number,b in number,c out number)
is
begin
c := a - b;
end subr;
declare
a number :=4;
b number :=2;
c number;
begin
  subr(a,b,c);
  dbms_output.put_line(a || ' - ' || b || ' = '|| c);
end;
-- assigning values in function
create or replace procedure addit(a out number,b out number,c out number)
is
begin
	a := 2;
	b := 3;
	c := a + b;
	dbms_output.put_line(a || ' + ' || b || ' = '|| c);
end addit;
declare
a number;
b number;
c number;
begin
    addit(a,b,c);
end;
-- by execute command/function we can run code
execute addit;
---- pl/sql  functions
create or replace function additi(a in number,b in number) return number
is
c number; 
begin
	c := a + b;
    return c;
end additi;
declare
a number;
b number;
c number;
begin
    c:= additi(7,2);
    dbms_output.put_line(c);
    dbms_output.put_line(a || ' + ' || b || ' = '|| c); --  not printing a and b values 
end;
-- 
create or replace function addition(a in number,b in number) return number
is
c number; 
begin
	c := a + b;
    return c;
end addition;
declare
a number := 24;
b number := 10;
c number;
begin
    c:= addition(a,b);
    dbms_output.put_line(a || ' + ' || b || ' = '|| c);
end;
 --local subprograms 
create table emplooyees (emp_id number,emp_name varchar2(100));
insert into emplooyees values (2,'loa');
select * from emplooyees where emp_id = 2;
declare
    function get_empl (empl_num emplooyees.emp_id%type) return emplooyees%rowtype is empl emplooyees%rowtype;
begin
 select *  into empl from emplooyees where emp_id = 2;
 return empl;
end;
    procedure insert_ele (emp_id emplooyees.emp_id%type) is empl emplooyees%rowtype;
begin
    empl := get_empl(emp_id);
    insert into emplooyees values empl;
end;
begin
  for re_emp in (select * from emplooyees ) loop
    if re_emp.emp_name = 'abc' then
      insert_ele (re_emp.emp_id);
    end if;
   end loop;
end;
-- overloading sub programs alias assigning same name to the existed function/procedure/subprogram
declare
    procedure insert_ele (p_emp_id emplooyees%rowtype) is empl emplooyees%rowtype;
    em_id number;
    function get_empl (pempl_num emplooyees.emp_id%type) return emplooyees%rowtype is empl emplooyees%rowtype;
begin
 select *  into empl from emplooyees where emp_id = 2;
 return empl;
end;
begin
    empl := get_empl(p_emp_id.emp_id);
    insert into emplooyees values empl;
end;
begin
  for re_emp in (select * from emplooyees ) loop
    if re_emp.emp_name = 'abc' then
      insert_ele (re_emp);
    end if;
   end loop;
end;
--handling exceptions in subprograms
--with above  calling get_empl function
declare
  va_emp emplooyees%rowtype;
begin
  va_emp := get_empl(1);
  dbms_output.put_line(va_emp.emp_name);
exception
     when others then
     dbms_output.put_line('oracle error');
end;
--regular and pipelined table functions
create type ty_day as object (va_date date,va_day_num int);
create type ty_days_table is table of ty_day;
create or replace function fi_get_day (p_str_date date,p_day_num int) return ty_days_table is
va_days ty_days_table := ty_days_table();
begin
  for k in 1..p_day_num loop
   va_days.extend;
   va_days(k) := va_days(p_str_date + k,to_number(to_char(p_str_date + k,'DDD')));
  end loop;
return va_days;
end;
-- pl/sql package
-- procedure package
-- assigning values at declare
create or replace package addit as
     procedure addi(a in number,b in number , c out number);
end addit;
create or replace package body addit as
   procedure addi(a in number,b in number, c out number) is
su  number;
begin
  su := a +  b ;
  dbms_output.put_line(su);
end addi;
end addit;
declare
   a number := 1;
   b number := 2;
   c number;
   su number;
begin
   addit.addi(a,b,c);
   dbms_output.put_line('');
   dbms_output.put_line(a || ' + '|| b || ' = ' ||  su);
end;
-- assigning values in procedure
create or replace package addit as
     procedure addi(a in number,b in number , c out number);
end addit;
create or replace package body addit as
   procedure addi(a in number,b in number, c out number) is
su  number;
begin
  su := a +  b ;
  dbms_output.put_line(su);
end addi;
end addit;
declare
   a number ;
   b number ;
   c number;
   su number;
begin
   addit.addi(12,37,c);
   dbms_output.put_line('');
   dbms_output.put_line(a || ' + '|| b || ' = ' ||  su);
end;
--function package 
-- assigning values at declare
create or replace package additi as
     function addit(a in number,b in number) return number;
end additi;
create or replace package body additi as
   function addit(a in number,b in number) return number is  
    su number;    
begin
  su := a +  b ;
  return su;
end addit;
end additi;
declare
   a number := 1;
   b number := 2;
   su number;
begin
   su := additi.addit(a,b);
   dbms_output.put_line('');
   dbms_output.put_line(a || ' + '|| b || ' = ' ||  su);
end;
----- assigning values in function
create or replace package additi as
     function addit(a in number,b in number) return number;
end additi;
create or replace package body additi as
   function addit(a in number,b in number) return number is  
    su number;    
begin
  su := a +  b ;
  return su;
end addit;
end additi;
declare
   a number;
   b number;
   su number;
begin
   su := additi.addit(19,57);
   dbms_output.put_line('');
   dbms_output.put_line(a || ' + '|| b || ' = ' ||  su);
end;
--calling procedure
declare
   a number := 1657;
   b number := 2460;
   c number;
   su number;
begin
   addit.addi(a,b,c);
   dbms_output.put_line('');
   dbms_output.put_line(a || ' + '|| b || ' = ' ||  su);
end;
--
declare
   a number ;
   b number ;
   c number;
   su number;
begin
   addit.addi(12718,2178637,c);
   dbms_output.put_line('');
   dbms_output.put_line(a || ' + '|| b || ' = ' ||  su);
end;
-- calling function
declare
   a number := 132467;
   b number := 2634;
   su number;
begin
   su := additi.addit(a,b);
   dbms_output.put_line('');
   dbms_output.put_line(a || ' + '|| b || ' = ' ||  su);
end;
--
declare
   a number;
   b number;
   su number;
begin
   su := additi.addit(19867,421357);
   dbms_output.put_line('');
   dbms_output.put_line(a || ' + '|| b || ' = ' ||  su);
end;
----
—pl/sql
CREATE OR REPLACE PACKAGE salary_package AS
  -- Function to calculate salary increments by designation
  FUNCTION calculate_increment(p_designation IN VARCHAR2, p_salary IN NUMBER) RETURN NUMBER;
  -- Procedure to update salary in a table
  PROCEDURE update_salary(p_employee_id IN NUMBER, p_salary IN NUMBER);
END salary_package;
/
CREATE OR REPLACE PACKAGE BODY salary_package AS
  -- Function to calculate salary increments by designation
  FUNCTION calculate_increment(p_designation IN VARCHAR2, p_salary IN NUMBER) RETURN NUMBER IS
    v_increment NUMBER;
  BEGIN
    IF p_designation = 'C1' THEN
      v_increment := p_salary * 0.05;
    ELSIF p_designation = 'C2' THEN
      v_increment := p_salary * 0.08;
    ELSIF p_designation = 'C3' THEN
      v_increment := p_salary * 0.1;
    ELSIF p_designation = 'C4' THEN
      v_increment := p_salary * 0.12;
    ELSIF p_designation = 'C5' THEN
      v_increment := p_salary * 0.15;       
    ELSE
      dbms_output.put_line('no increment');
    END IF;
    RETURN v_increment;
  END;
  -- Procedure to update salary in a table
  PROCEDURE update_salary(p_employee_id IN NUMBER, p_salary IN NUMBER) IS
  BEGIN
    UPDATE Employee
    SET salary = p_salary
    WHERE Employee_id = p_employee_id;
    COMMIT;
  END;
END salary_package;
DECLARE
  v_salary NUMBER;
BEGIN
  -- Calculate salary increment for a manager
  v_salary := salary_package.calculate_increment('C1', 10000);
  DBMS_OUTPUT.PUT_LINE('Salary increment for Manager: ' || v_salary);  
  -- Update salary for an employee
  salary_package.update_salary(1001, 11000);
  DBMS_OUTPUT.PUT_LINE('Salary updated successfully');
END;
-- in oracle developer we can right click and add new trigger at trigger function
-- while creating in dialogue box we need to fill schem,name,type,time,event,columns 
create table employees(employee_id number,employee_name varchar2(10))
insert into employees values (2,'jshdgf');
/* ******"No need to type query by selecting in trigger create dialogue box we get this query when we click that trigger
or we can type its our choice to type or select.""****** */
create or replace trigger name_trigger
    before insert or update or delete on employees
begin
  dbms_output.put_line('trigger');
end;
-- before statement trigger
create or replace trigger before_statement_trigger
    before insert or update on employees
begin
  dbms_output.put_line('before statement trigger');
end;
-- after statement
create or replace trigger after_statement_trigger
    after insert or update or delete on employees
begin
  dbms_output.put_line('after statement trigger');
end;
-- for each row
create or replace trigger after_foreach_statement_trigger
    after insert or update or delete on employees
    for each row
begin
  dbms_output.put_line('after statement for each trigger');
end;
--
create or replace trigger before_foreach_statement_trigger
    before insert or update or delete on employees
    for each row
begin
  dbms_output.put_line('before statement for each trigger');
end;
-- in schema we create triggers in that triggers we type/choose trigger statements 
-- in main schema we write queries and in in triggers menu we write triggers
update employees set employee_name = 'gfvzhfg' where employee_id =2;
insert into employees values (3,'fgeyig')
delete employees where employee_id =3;
-- got output and updated
select * from employees;
-- new and old qualifiers in triggers
alter table employees disable all triggers;
create or replace trigger new_old_statement_trigger
    before insert or update or delete on employees
    for each row
begin
  dbms_output.put_line('before statement for each trigger');
  dbms_output.put_line('before update '|| :old.employee_name || ' after update ' || :new.employee_name );
end;
-- conditional predicates
-- if we insert/update/delete line by line decreases the performance so we use conditional predicates
create or replace trigger conditional_predicates_statement_trigger
    before insert or update or delete on employees
    for each row
begin
  dbms_output.put_line('before statement for each trigger');
  dbms_output.put_line('before update '|| :old.employee_name || ' after update ' || :new.employee_name );
  if inserting then
      dbms_output.put_line('inserted in table');
  elsif updating then
      dbms_output.put_line('updated in table');
  elsif deleting then
      dbms_output.put_line('deleted in table');
  end if;
end;
----
update employees set employee_name = 'ewiajsewu' where employee_id =4;
insert into employees values (4,'fghe')
delete employees where employee_id =4;
select * from employees;
create table employees(emp_id number,emp_name varchar2(20))
insert into employees values (1,'hka')
alter table employees add emp_age number
insert into employees values (2,'dfhj',24)
insert into employees values (3,'ngzggn',27) 
update employees set emp_age = 23 where emp_id =1
select * from employees
-- raise_application_statement_trigger 
create or replace trigger raise_application_statement_trigger 
    before insert or update or delete on employees 
    for each row 
begin 
  dbms_output.put_line('before statement for each trigger'); 
  dbms_output.put_line('before update '|| :old.emp_name || ' after update ' || :new.emp_name ); 
  if inserting then 
    if :new.emp_age > 23 then 
     raise_application_error(-2000,'you cant insert'); 
    end if; 
    dbms_output.put_line('inserted in table'); 
  elsif updating then 
      dbms_output.put_line('updated in table'); 
  elsif deleting then 
      dbms_output.put_line('deleted in table'); 
  end if; 
end;
--
insert into employees values (4,'fgilq',19) 
create or replace trigger raise_application_statement_trigger 
    before insert or update or delete on employees 
    for each row 
begin 
  dbms_output.put_line('before statement for each trigger'); 
  dbms_output.put_line('before update '|| :old.emp_name || ' after update ' || :new.emp_name ); 
  if inserting then 
    if :new.emp_age > 23 then 
     raise_application_error(-2000,'you cant insert'); 
    end if; 
    dbms_output.put_line('inserted in table'); 
  elsif updating then 
      if :new.emp_age > 23 then 
     raise_application_error(-2000,'you cant insert'); 
      end if; 
      dbms_output.put_line('updated in table'); 
  elsif deleting then 
      dbms_output.put_line('deleted in table'); 
  end if; 
end;
---
update employees set emp_age = 20 where emp_id =4
-- updateof_event_statement_trigger 
-- we can update any column
create or replace trigger updateof_event_statement_trigger 
    before insert or update or delete on employees 
    for each row 
begin 
  dbms_output.put_line('before statement for each trigger'); 
  dbms_output.put_line('before update '|| :old.emp_name || ' after update ' || :new.emp_name ); 
  if inserting then 
    if :new.emp_age > 23 then 
     raise_application_error(-2000,'you cant insert'); 
    end if; 
    dbms_output.put_line('inserted in table'); 
  elsif updating ('emp_age') then 
      if :new.emp_age > 23 then 
     raise_application_error(-2000,'you cant insert'); 
      end if; 
      dbms_output.put_line('updated in table'); 
  elsif deleting then 
      dbms_output.put_line('deleted in table'); 
  end if; 
end;
--
create or replace trigger updateof_event_statement_trigger 
    before insert or update or delete on employees 
    for each row 
begin 
  dbms_output.put_line('before statement for each trigger'); 
  dbms_output.put_line('before update '|| :old.emp_name || ' after update ' || :new.emp_name ); 
  if inserting then 
    if :new.emp_age > 23 then 
     raise_application_error(-2000,'you cant insert'); 
    end if; 
    dbms_output.put_line('inserted in table'); 
  elsif updating then 
      if updating ('emp_name') then 
       raise_application_error(-2000,'you cant update'); 
      end if; 
      dbms_output.put_line('updated in table'); 
  elsif deleting then 
      dbms_output.put_line('deleted in table'); 
  end if; 
end;
--
create or replace trigger updateof_event_statement_trigger 
    before insert or update or delete on employees 
    for each row 
begin 
  dbms_output.put_line('before statement for each trigger'); 
  dbms_output.put_line('before update '|| :old.emp_name || ' after update ' || :new.emp_name ); 
  if inserting then 
    if :new.emp_age > 23 then 
     raise_application_error(-2000,'you cant insert'); 
    end if; 
    dbms_output.put_line('inserted in table'); 
  elsif updating ('emp_age') then 
      if :new.emp_age > 23 then 
     raise_application_error(-2000,'you cant insert'); 
      end if; 
      dbms_output.put_line('updated in table'); 
  elsif deleting then 
      dbms_output.put_line('deleted in table'); 
  end if; 
end;
--when triggers
create or replace trigger when_clause_trigger 
    before insert or update on employees 
    for each row 
    when (new.emp_age > 23)  
begin 
  raise_application_error(-20006,'you cant assign graeter than age 23'); 
end;
-- instead of
create table employees1 as select * from employees
select * from employees inner join employees1 on employees.emp_id = employees1.emp_id
create or replace view abc as  select * from employees --inner join employees1 on employees.emp_id = employees1.emp_id
-- instead of used when it is complex
create or replace trigger Instead_of 
    instead of  insert or update or delete on abc 
    for each row 
declare 
    v number; 
begin 
     if inserting then 
        select emp_name into v from employees; 
        insert into employees values (v,:new.emp_name,null); 
     elsif deleting then 
         delete from employees where emp_id =1; 
     elsif updating ('emp_name') then  
          update employees set emp_name = 'dfhgfh' where emp_id =2; 
     else 
       raise_application_error(-20007,'instead of '); 
     end if; 
end;
-- exploring and managing triggers
select * from user_triggers
alter trigger Instead_of enable 
alter trigger Instead_of disable 
alter table employees enable all triggers 
alter table employees disable all triggers 
alter trigger Instead_of enable 
alter trigger Instead_of compile 
drop trigger Instead_of 
-- disable triggers
create or replace trigger disable_triggers 
  before  insert or update or delete on employees 
  for each row 
  disable  
begin 
     dbms_output.put_line('disabling trigger always on disable until we enable disable triggers wont affect tables and vies'); 
end; 









                                               



