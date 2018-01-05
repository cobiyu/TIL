**Function**
====

- cursor를 이용한 function
    - 다단일 레코드가 아닌 여러행으로 구성된 작업영역에서 SQL 결과를 저장하기 위해 커서를 사용
    ```sql
    CREATE OR REPLACE Function TotalIncome
       ( name_in IN varchar2 )  -- 변수선언
       RETURN varchar2
    IS
       total_val number(6);

       cursor c1 is -- c1 커서변수 (loop용 변수)
         SELECT monthly_income
         FROM employees
         WHERE name = name_in;

    BEGIN

       total_val := 0;

       FOR employee_rec in c1   --FOR를 이용한 loop(foreach방식)
           LOOP
              total_val := total_val + employee_rec.monthly_income;
           END LOOP;

       RETURN total_val;

    END;
    ```
    
- SYS_REFCURSOR를 이용한 function 
    - SYS_REFCURSOR는 쿼리 실행 결과를 저장하기 위한 자료형이다.

    ```sql
    CREATE OR REPLACE PROCEDURE listAllScore (
        pResult OUT SYS_REFCURSOR
    )
    IS
    BEGIN
        OPEN pResult FOR
            SELECT hak, name, birth, kor, eng, mat,
                kor+eng+mat AS total, (kor+eng+mat)/3 AS avg,
                  rank() OVER(ORDER BY (kor+eng+mat) DESC) AS rank
            FROM score;
    END;
    /

    -- 위에서 만든 프로시저를 확인하기 위한 프로시저
    CREATE or replace procedure s4
    IS
          result SYS_REFCURSOR; --  쿼리실행결과 저장 위한 변수
          vHak VARCHAR2(20);
          vName VARCHAR2(20);
          vBirth VARCHAR2(30);
          vKor NUMBER;
          vEng NUMBER;
          vMat NUMBER;
          vTotal NUMBER;
          vAvg NUMBER;
          vRank NUMBER;
    BEGIN
         -- 프로시저 호출
          listAllScore(result);
        LOOP
            FETCH result INTO vHak, vName, vBirth, vKor, vEng, vMat, vTotal, vAvg, vRank;
            EXIT WHEN result%notfound;
            DBMS_OUTPUT.PUT_LINE(vName || ' ' || vTotal);
        END LOOP;
    END;
    /
    ```