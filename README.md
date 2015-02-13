# Packages-and-Cursors

Used Cursors and created a package that included stored procedures to implement join on 2 tables without using a join query.



\*---------------------------------------------------------Code------------------------------------------------------------*/


CREATE OR REPLACE PACKAGE ASSIGNMENT AS 
 
 procedure ROHITH;
  /* TODO enter package declarations (types, exceptions, methods etc) here */
  

END ASSIGNMENT;
/


CREATE OR REPLACE PACKAGE BODY ASSIGNMENT AS 
PROCEDURE ROHITH AS
  cursor dept_cur
        is select *
              from departments;
     d dept_cur%rowtype;
     cursor emp_cur( p_department_id IN departments.department_id%type )
       is select *
              from employees
            where department_id = p_department_id;
        
     e emp_cur%rowtype;
   begin
    open dept_cur;
     loop
       fetch dept_cur into d;
       exit when dept_cur%notfound;
       open emp_cur( d.department_id );
      loop
         fetch emp_cur into e;
         exit when emp_cur%notfound;
         dbms_output.put_line( 'Employee ' || e.employee_id || ' ' || e.first_name ||' ' || e.last_name ||
                               ' in department ' || d.department_name );
       end loop;
       close emp_cur;
     end loop;
    close dept_cur;
 end ROHITH;
 end ASSIGNMENT;
/
exec assignment.rohith;
