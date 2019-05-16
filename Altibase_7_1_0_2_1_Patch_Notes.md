Altibase 7.1.0.2.1 Patch Notes
==============================

New Features
------------

### BUG-46702 C사 rollup syntax 지원

-   **module** : qp-dml-execute

-   **Category** : Other

-   **재현 빈도** : Always

-   **증상** : C사 rollup syntax 지원

-   **재현 방법**

    -   **재현 절차**

    -   **수행 결과**

    -   **예상 결과**

-   **Workaround**

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-46703 limit clause에 simple expression 지원.

-   **module** : qp-dml-pvo

-   **Category** : Functionality

-   **재현 빈도** : Always

-   **증상** : Limit clause에 연산, function 호출, package 변수
    접근 등이 가능하도록 개선합니다.

-   **재현 방법**

    -   **재현 절차**

            iSQL> select * from t1 limit 1+1;
            [ERR-31001 : SQL syntax error
            line 1: parse error
            select * from T1 limit 1+1

    -   **수행 결과**

    -   **예상 결과**

            iSQL> select * from t1 limit 1+1;I1          I2---------------------------1           12           22 rows selected.

-   **Workaround**

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-46719 C사 SYSDATETIME 지원

-   **module** : qp

-   **Category** : Other

-   **재현 빈도** : Always

-   **증상** : SYSDATETIME을 지원합니다.

    altibase의 SYSDATE와 동일하며, 운영중인 시스템의 현재시간 날짜
    출력합니다.

-   **재현 방법**

    -   **재현 절차**

            iSQL> select sysdatetime from dual;[ERR-31058 : Column not found0001 : select SYSDATETIME from DUAL             ^^]

    -   **수행 결과**

    -   **예상 결과**

            iSQL> select sysdatetime from dual;SYSDATETIME---------------21-JAN-20191 row selected.

-   **Workaround**

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-46727 ISO 표준 기준 년 IYYY format 지원

-   **module** : mt-function

-   **Category** : Functionality

-   **재현 빈도** : Always

-   **증상** : DATE를 문자열로 표현할 때, IYYY IYY IY I 형식을
    추가합니다.

    ​1. SQL (TO\_CHAR FUNCTION)

        SELECT TO\_CHAR( date, 'IYYY' ) FROM T1 ORDER BY I1;

    ​2. SQL (DATE -\> CHAR ENCODE)

        ALTER SESSION SET DEFAULT\_DATE\_FORMAT = 'IYYY';

        SELECT date FROM T1 ORDER BY I1;

    ​3. CLI (DATE -\> CHAR CONVERT)

        (1) SQLDriverConnect   : DATE\_FORMAT=IYYY

        (2) Query              : SELECT date FROM T1 ORDER BY I1

        (3) SQLBindCol & Fetch : SQL\_C\_CHAR

-   **재현 방법**

    -   **재현 절차**

            iSQL> SELECT TO_CHAR(TO_DATE('2018-12-31','YYYY-MM-DD'), 'IYYY-IW') FROM DUAL;[ERR-21039 : The date format ( IYYY-IW ) was not recognized. 0001 : SELECT TO_CHAR(TO_DATE('2018-12-31','YYYY-MM-DD'), 'IYYY-IW') FROM DUAL             ^                                                     ^]

    -   **수행 결과**

            [ERR-21039 : The date format ( IYYY-IW ) was not recognized. 0001 : SELECT TO_CHAR(TO_DATE('2018-12-31','YYYY-MM-DD'), 'IYYY-IW') FROM DUAL             ^                                                     ^

    -   **예상 결과**

            SQL> SELECT TO_CHAR(TO_DATE('2018-12-31','YYYY-MM-DD'), 'IYYY-IW') FROM DUAL; TO_CHAR(TO_DAT--------------2019-01

-   **Workaround**

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-46755 호스트 네임으로 발급된 라이선스 적용

-   **module** : id

-   **Category** : Other

-   **재현 빈도** : Always

-   **증상** : 라이센스정책 변경(hostname으로도 License 발급가능)으로
    변경된 라이선스가 적용되도록 수정하였습니다. 기존에 MAC Address 를
    기반으로 License 를 발급하였는데,

    MAC Address 또는 HOST Name 을 이용해서 License 를 발급할 수 있도록
    변경되었습니다.

-   **재현 방법**

    -   **재현 절차**

    -   **수행 결과**

    -   **예상 결과**

-   **Workaround**

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-46781 이중화 DDL 안전성 개선

-   **module** : rp

-   **Category** : Enhancement

-   **재현 빈도** : Always

-   **증상** : 이중화 DDL 안전성 향상을 위한 개선사항을 적용합니다.

-   **재현 방법**

    -   **재현 절차**

    -   **수행 결과**

    -   **예상 결과**

-   **Workaround**

-   **변경사항**
    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code
        -   399,rpERR\_ABORT\_FAULT\_TOLERATED = Failed to work because
            an internal exception occurred from an OS.[Contact
            Altibase's Support Center]
             \# \*Cause: An internal exception occurred from an OS.
             \# \*Action: Check the error number from the trace log for
            more detailed information. And contact Altibase's Support
            Center (http://support.altibase.com).

### BUG-46825 OTHER\_DATABASE\_SKIP\_ERROR 와 ORACLE\_SKIP\_ERROR 정책변경 따라 수정이 필요 합니다.

-   **module** : rp-jdbcAdapter

-   **Category** : Other

-   **재현 빈도** : Always

- **증상** : OTHER_DATABASE_SKIP\_ERROR = 0 , ORACLE_SKIP_ERROR=0 인 경우, 기본적으로 에러를 스킵하지않되, 스킵해야하는 에러코드들을 dbms\_skip\_error\_include.list 에
  기록할수 있도록 했습니다.

  OTHER_DATABASE_SKIP\_ERROR = 1 , ORACLE_SKIP_ERROR=1 인 경우, 기본적으로 에러를 스킵하되, 스킵하면 안되는 에러코드들을 dbms\_skip\_error\_exclude.list 에 기록할수
  있도록 했습니다.

-   **재현 방법**

    -   **재현 절차**

    -   **수행 결과**

    -   **예상 결과**

-   **Workaround**

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-46832 memory partition table 의 simple query 최적화

- **module** : qp

- **Category** : Enhancement

- **재현 빈도** : Always

- **증상** : 기존에는 memory table에 대해서만 simple query 최적화를
  지원하였으나, memory partition table 의 경우도 지원하도록
  수정하였습니다.

  프로퍼티 EXECUTOR\_FAST\_SIMPLE\_QUERY =2 인경우에 사용가능합니다

- **재현 방법**

  -   **재현 절차**

  -   **수행 결과**

  -   **예상 결과**

- **Workaround**

- **변경사항**

  - Performance view

  - Property

  - Compile Option

  - Error Code

    ### BUG-46806 INSERT 구문에 alias 지원

    - **module** : qp-dml-execute

    - **Category** : Other

    - **재현 빈도** : Always

    - **증상** :

    - **재현 방법**

      - **재현 절차**

        ```
        iSQL> insert into t1 a (a.i1) values (1);
        [ERR-31001 : SQL syntax error
        line 1: parse error
        insert into T1 A (A.I1) values (1)
                                       ^
        ]
        ```

      - **수행 결과**

      - **예상 결과**

        ```
        iSQL> insert into t1 a (a.i1) values (1);1 row inserted.
        ```

    - **Workaround**

    - **변경사항**

      - Performance view
      - Property
      - Compile Option
      - Error Code

Fixed Bugs
----------

### BUG-46208 REPLICATION\_SENDER\_AUTO\_START 값이 설정되어 있는 상태에서 서버 시작를 못할수 있습니다.

-   **module** : rp

-   **Category** : Functional Error

-   **재현 빈도** : Rare

-   **증상** : 이중화 start시에 lock timeout을 0으로 해서 table lock을
    바로 획득하지 못하면 실패하도록 되어있습니다.

    Server start시 REPLICATION\_SENDER\_AUTO\_START가 설정되어 있으면
    이중화를 자동으로 start 시키는데

    receiver에서 table에 data를 execute 하기위해 lock을 잡고
    있면 sender가 start중 lock을 획득하지 못해 실패하게되고

    이로인해 server start도 실패 하게 됩니다.

    server start중에 이중화 sender를 start 시키는 경우에는 lock
    timeout을 무한대로 설정하여 receiver가 lock을 반환 할때 까지
    대기해서 server start가 실패하지 않도록 수정하였습니다.

-   **재현 방법**

    -   **재현 절차**

    -   **수행 결과**

    -   **예상 결과**

-   **Workaround**

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-46647 msg에서 LSN의 Global No 를 제거해야 합니다.

-   **module** : sm\_resource

-   **Category** : Message Error

-   **재현 빈도** : Always

-   **증상** :

-   **재현 방법**

    -   **재현 절차**

    -   **수행 결과**

    -   **예상 결과**

-   **Workaround**

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-46670 temp flusher에서 이미 free된 temp table header에 접근 할 수 있습니다.

-   **module** : sm-disk-resource

-   **Category** : Fatal

-   **재현 빈도** : Unknown

-   **증상** : disk temp table에서 stress test 중에 통계정보 이슈로 temp
    table header 를 해제하고 나서 접근하는 문제가 있어서 해결
    하였습니다.

-   **재현 방법**

    -   **재현 절차**

    -   **수행 결과**

    -   **예상 결과**

-   **Workaround**

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-46680 INSERT\_REPLACE가 1로 되어 있을때 CLOB이 포함된 Table에 Replcation SYNC를 두번 수행하면 lock timeout이 발생합니다.

-   **module** : dm

-   **Category** : Other

-   **재현 빈도** : Always

-   **증상** : INSERT\_REPLACE가 1로 되어 있을때 LOB이 포함된 Table에서
    Replcation SYNC를 두 번 수행하면 lock timeout이 발생하는 문제가
    있어, 이를 수정하였습니다.

-   **재현 방법**

    -   **재현 절차**

    -   **수행 결과**

    -   **예상 결과**

-   **Workaround**

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-46697 hash partition 이중화 시 이중화 재시작을 하면 partition 갯수를 찾지 못해 handshake 가 되지 않습니다.

-   **module** : rp

-   **Category** : Testcase Fail

-   **재현 빈도** : Always

-   **증상** : 해시 파티션 이중화시 이중화를 중지했다가 재시작 하면 해시 파티션 갯수를 잘못 계산하여
    이중화가 되지 않는 문제가 있습니다. 이중화 재 시작시에 해시파티션 갯수를 바르게 찾아 이중화가 진행되도록 수정하였습니다.

-   **재현 방법**

    -   **재현 절차**

    -   **수행 결과**

    -   **예상 결과**

-   **Workaround**

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-46700 메모리 테이블의 LOB컬럼 UPDATE시 메모리 테이블 사이즈가 계속 증가할 수 있는 문제 수정

-   **module** : sm

-   **Category** : Functional Error

-   **재현 빈도** : Always

-   **증상** : 메모리 테이블의 LOB컬럼 UPDATE시

    메모리 테이블 사이즈가 계속 증가할 수 있는 문제가 있어서
    수정하였습니다.

-   **재현 방법**

    -   **재현 절차**

    -   **수행 결과**

    -   **예상 결과**

-   **Workaround**

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-46708 윈도우 OS에서는 altilinker 실행시 java파일이 아니라 java.exe파일을 찾도록 수정해야 합니다.

-   **module** : dblink

-   **Category** : Other

-   **재현 빈도** : Always

-   **증상** : 윈도우 OS에서는 java파일이 아니라 java.exe 파일이
    존재하여 dblink 실행시 java파일이 없는 것으로 판단하여
    에러가 발생하였습니다.

    윈도우 OS에서는 java 파일이 아니라 java.exe 파일로 java 유무를
    판단하도록 수정하였습니다.

-   **재현 방법**

    -   **재현 절차**

            dblink enable 후 server start

    -   **수행 결과**

            java 파일을 찾지 못하여 에러 발생

    -   **예상 결과**

            서버와 altilinker 정상적으로 구동

-   **Workaround**

        java.exe 파일을 복사하여 java파일을 만든다.

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-46728 order by 절에 사용된 host 변수를 target과 같은 varchar로 지정하도록 수정

-   **module** : qp-dml-execute

-   **Category** : Other

-   **재현 빈도** : Always

-   **증상** : order by 절에 사용된 host 변수를 target과 같은 varchar로
     지정하도록 수정

- **재현 방법**

  - **재현 절차**

        iSQL> VAR V1 VARCHAR(100);
        iSQL> EXEC :V1 := 'KO';
        Execute success.
        iSQL> print var;
        [ HOST VARIABLE ]
        -------------------------------------------------------
        NAME                 TYPE                 VALUE
        -------------------------------------------------------
        V1                   VARCHAR(100)         KO
        iSQL> PREPARE SELECT CASE WHEN :v1 ='KO' THEN 1 ELSE 2 END FROM DUAL; CASEWHEN:V1='KO'THEN1ELSE2END 
        --------------------------------
        1           
        1 row selected.
        iSQL> PREPARE SELECT CASE WHEN :v1 ='KO' THEN 1 ELSE 2 END FROM DUAL ORDER BY (CASE WHEN :v1 ='KO' THEN 1 ELSE 2 END);
        [ERR-3123B : Invalid use of host variables 
        0001 : SELECT CASE WHEN :v1 ='KO' THEN 1 ELSE 2 END FROM DUAL ORDER BY (CASE WHEN :v1 ='KO' THEN 1 ELSE 2 END)

  -   **수행 결과**

  - **예상 결과**

        iSQL> VAR V1 VARCHAR(100);
        iSQL> EXEC :V1 := 'KO';
        Execute success.
        iSQL> print var;
        [ HOST VARIABLE ]
        -------------------------------------------------------
        NAME                 TYPE                 VALUE
        -------------------------------------------------------
        V1                   VARCHAR(100)         KO
        iSQL> PREPARE SELECT CASE WHEN :v1 ='KO' THEN 1 ELSE 2 END FROM DUAL; CASEWHEN:V1='KO'THEN1ELSE2END 
        --------------------------------
        1           
        1 row selected.
        iSQL> PREPARE SELECT CASE WHEN :v1 ='KO' THEN 1 ELSE 2 END FROM DUAL ORDER BY (CASE WHEN :v1 ='KO' THEN 1 ELSE 2 END);
        CASEWHEN:V1='KO'THEN1ELSE2END 
        --------------------------------
        1           
        1 row selected.

-   **Workaround**

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-46731 simple query를 사용하는 insert문에도 nowait에 대한 고려가 필요합니다.

-   **module** : qp

-   **Category** : Functional Error

-   **재현 빈도** : Always

-   **증상** : simple query를 사용하는 insert문에서 nowait이 적용되지
    않는 문제를 수정하였습니다.

-   **재현 방법**

    -   **재현 절차**

    -   **수행 결과**

    -   **예상 결과**

-   **Workaround**

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-46754 server restart 시 logfile0 이 없어서 서버가 시작 하지 못 합니다.

-   **module** : sm

-   **Category** : Fatal

-   **재현 빈도** : Rare

-   **증상** : 리커버리 시작위치에 고려해야하는
    요소가 추가되었으나 불필요한 로그파일 제거 루틴에서는 추가된 요소에 대한 처리가 누락되었습니다. 해당 요소를 고려하도록 수정합니다.

-   **재현 방법**

    -   **재현 절차**

    -   **수행 결과**

    -   **예상 결과**

-   **Workaround**

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-46757 V\$DB\_PROTOCOL 조회시 이상한 문자가 출력됩니다.

-   **module** : cm

-   **Category** : Functional Error

-   **재현 빈도** : Always

-   **증상** : V\$DB\_PROTOCOL 조회시 추가된 프로토콜에 대한 정의가
    코드상에서 빠져 있어

    이상한 문자열이 출력 되는 문제가 존재 하였습니다.

    그래서 추가된 프로토콜에 대하여 정의를 코드상에서 추가 하였습니다.

- **재현 방법**

  -   **재현 절차**

          select * from v$db_protocol;

  - **수행 결과**

        CMP_OP_DB_ShardNodeGetListResult                    92        
        0                    
        CMP_OP_DB_ShardHandshake                            93        
        0                    
        CMP_OP_DB_ShardHandshakeResult                      94        
        0                    
        CMP_OP_DB_MAX                                       95        
        0                    
        UH‰�Hƒ�0H‰}�H‹E�Hƒ�H‰E�H‹E�H‰험�                  96  
        0                    
        UH‰�Hƒ�0H‰}�H‹E�Hƒ�H‰E�H‹E�HƒH‰험h�      97          
        0                    
        UH‰�H‰}片                                           98       
        0                    
        UH‰�Hƒ�0H‰}�H‹E�Hƒ�H‰E�H‹E�HƒH‰험곁              99    
        0                    
        UH‰�Hƒ�@H‰}�H‹E�Hƒ�H‰E�H‹E�H‰험晦                  100 
        0                    
        101 rows selected.

  -   **예상 결과**

          Correct protocols.

-   **Workaround**

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-46782 Begin transaction 디버깅 정보 추가.

-   **module** : sm\_transaction

-   **Category** : Fatal

-   **재현 빈도** : Rare

-   **증상** : altibase\_error.log 로그에 Invalid statement processing
    request 오류가 발생할 수 있어서, 디버깅 정보를 추가하였습니다.

    smxTrans::begin()에서 문제 발생 시 디버깅 정보를 기록하여,

    ​1. begin된 transaction을 정리하지 않고 재활용 한 것인지,

    ​2. free된 transaction을 잘못 건드린 것인지,

    ​3. smiTrans에서 transaction Pool에서 최초 할당 받았는데, 문제가
    있는 것인지,

    ​4. 혹은 smiTrans에서 기존 transaction을 정리 없이 재활용 한 것인지
    등등

    비정상 종료 시 출력한 디버깅 정보를 기준으로 찾을 수 있도록 합니다.

-   **재현 방법**

    -   **재현 절차**

    -   **수행 결과**

    -   **예상 결과**

-   **Workaround**

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-46800 ANTI JOIN시 INVERSE HASH로 PLAN생성 시 CONSTANT FILTER 처리

-   **module** : qp-dml-pvo

-   **Category** : Other

-   **재현 빈도** : Always

-   **증상** : INVERSE HASH로 PLAN생성 시 CONSTANT FILTER 가 잘못
    처리되는 현상 수정

-   **재현 방법**

    -   **재현 절차**

            drop table t1;
            drop table t2;
            create table t1(i1 integer , i2 integer);
            create index t1_i2_idx on t1(i2);
            create table t2(i1 integer, i2 integer);
            create index t2_i2_idx on t2(i2); 
            insert into t1 select level, mod(level, 10)+1 from dual connect by level <= 100;
            insert into t1 values (999, 999);
            insert into t1 values (1000, null); 
            insert into t2 select level, level+1 from dual connect by level <= 20;
            insert into t2 values (99, 99);
            insert into t2 values (100, null);
            iSQL> SELECT t1.*
                2   FROM t1
                3  WHERE 'N' = 'Y' AND NOT EXISTS (SELECT  /*+ INVERSE_JOIN */  1
                4                      FROM t2
                5                     WHERE t2.i1 = t1.i2);
                I1          I2
            ---------------------------
            ...
            102 rows selected.

    -   **수행 결과**

    -   **예상 결과**

            iSQL> SELECT t1.*    2   FROM t1    3  WHERE 'N' = 'Y' AND NOT EXISTS (SELECT  /*+ INVERSE_JOIN */  1    4                      FROM t2    5                     WHERE t2.i1 = t1.i2);I1          I2---------------------------No rows selected.

-   **Workaround**

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-46805 target에 index를 타는 subquery 2개가 where문을 제외한 다른 부분이 같을 경우 결과 오류

-   **module** : qp-dml-execute

-   **Category** : Other

-   **재현 빈도** : Always

-   **증상** : taget에 index를 타는 subquery 2개가 where문을 제외한 다른
    부분이 같을 경우 결과 오류 수정

- **재현 방법**

  -   **재현 절차**

          drop table t1 cascade;
          create table t1(i1 integer , i2 integer);
          alter table t1 add constraint t1_pk primary key(i1);
          insert into t1 select level, 10 from dual connect by level <= 10;
          SELECT 
              MAX( ( SELECT COUNT(AA.I1) FROM T1 AA WHERE AA.I2=1 ))  as C1,
              MAX( ( SELECT COUNT(AA.I1) FROM T1 AA WHERE AA.I2=10 ))  as C2
          FROM DUAL;

  - **수행 결과**

        iSQL> SELECT
             MAX( ( SELECT COUNT(AA.I1) FROM T1 AA WHERE AA.I2=1 )) as C1,
             MAX( ( SELECT COUNT(AA.I1) FROM T1 AA WHERE AA.I2=10 )) as C2
             FROM DUAL;
        C1                   C2
        ---------------------------------------------
        0                    0
        1 row selected.

  - **예상 결과**

        iSQL> SELECT 
        	MAX( ( SELECT COUNT(AA.I1) FROM T1 AA WHERE AA.I2=1 ))  as C1,
            MAX( ( SELECT COUNT(AA.I1) FROM T1 AA WHERE AA.I2=10 ))  as C2
        FROM DUAL;
        C1                   C2
        ---------------------------------------------
        0                    10
        1 row selected.

-   **Workaround**

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-46816 table name과 username이 128자 이상일 경우 메모리 침범이 발생합니다.

-   **module** : dm

-   **Category** : Other

-   **재현 빈도** : Always

-   **증상** : table name과 username의 메모리 할당 사이즈를 작게
    할당하여 128자 이상일 경우 메모리 침범이 발생하였습니다.

    메모리 할당 사이즈를 늘여 주어 메모리 침범이 발생하지 않도록
    수정하였습니다.

-   **재현 방법**

    -   **재현 절차**

            n/a

    -   **수행 결과**

            n/a

    -   **예상 결과**

            n/a

-   **Workaround**

        n/a

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-46826 DDL PVO 안정성 개선

-   **module** : qp-ddl-dcl-pvo

-   **Category** : Functionality

-   **재현 빈도** : Always

-   **증상** : DDL PVO 수행 중 내부적인 요인에 의한 FATAL이 발생는 경우,
    비정상종료하지 않도록 개선되었습니다.

-   **재현 방법**

    -   **재현 절차**

    -   **수행 결과**

    -   **예상 결과**

-   **Workaround**

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-46836 simple query 최적화를 사용하는 환경에서 select for update 시에 nowait option 적용되지 않는 문제가 있습니다.

-   **module** : qp-select-execute

-   **Category** : Functional Error

-   **재현 빈도** : Always

-   **증상** : simple query 최적화를 사용하는 환경에서 select for update
    시에 nowait option 이 적용되지 않고, timeout 까지 대기하는 문제가
    있습니다. 이를 수정하였습니다.

-   **재현 방법**

    -   **재현 절차**

            include stdFunc.i;
            DEF MAIN ()
            {
                SKIP BEGIN;
                drop table t1;
                SKIP END;
                create table t1 (c1 int primary key, c2 char(200) );
                insert into t1 values (1,'1');
                commit;
                ALTER SYSTEM SET EXECUTOR_FAST_SIMPLE_QUERY = 0;
                THREAD T1 C0
                {
                    autocommit off;
                    select * from t1 where c1 =1 for update nowait;
                }
                THREAD T2 C0
                {
                    autocommit off;
                    select * from t1 where c1 =1 for update nowait;
                }
                JOIN;
                THREAD T1 C0
                {
                    rollback;
                }
                THREAD T2 C0
                {
                    rollback;
                }
                ALTER SYSTEM SET EXECUTOR_FAST_SIMPLE_QUERY = 1;
                THREAD T1 C0
                {
                    autocommit off;
                    select * from t1 where c1 =1 for update nowait;
                }
                THREAD T2 C0
                {
                    autocommit off;
                    select * from t1 where c1 =1 for update nowait;
                }
                JOIN;
                THREAD T1 C0
                {
                    rollback;
                }
                THREAD T2 C0
                {
                    rollback;
                }
                DROP TABLE T1;
            }

    -   **수행 결과**

             타임아웃때까지 대기

    -   **예상 결과**

            대기없이 실패

-   **Workaround**

        ALTER SYSTEM SET EXECUTOR_FAST_SIMPLE_QUERY = 0;

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

Changes
-------

### Version Info

  altibase version   database binary version   meta version   cm protocol version   replication protocol version   sharding version
------------------ ------------------------- -------------- --------------------- ------------------------------ ------------------
  7.1.0.1.8          6.5.1                     8.7.1          7.1.6                 7.4.4                          2.1.0

> Altibase 7.1 패치 버전별 히스토리는
> [Version\_Histories](https://github.com/ALTIBASE/Documents/blob/master/PatchNotes/Altibase_7_1_Version_Histories.md)
> 에서 확인할 수 있다.

### 호환성

#### Database binary version

데이터베이스 바이너리 버전은 변경되지 않았다.

> 데이터베이스 바이너리 버전은 데이터베이스 이미지 파일과 로그파일의
> 호환성을 나타낸다. 이 버전이 다른 경우의 패치(업그레이드 포함)는
> 데이터베이스를 재구성해야 한다.

#### Meta Version

메타 버전은 변경되지 않았다.

> 패치를 롤백하려는 경우,
> [메타다운그레이드](https://github.com/ALTIBASE/Documents/blob/master/Manuals/Altibase_7.1/kor/Installation.md#%EB%A9%94%ED%83%80-%EB%8B%A4%EC%9A%B4%EA%B7%B8%EB%A0%88%EC%9D%B4%EB%93%9Cmeta-downgrade)를
> 참고한다.

#### CM protocol Version

통신 프로토콜 버전은 변경되지 않았다.

#### Replication protocol Version

Replication 프로토콜 버전은 변경되지 않았다..

#### Sharding Version

샤딩 버전은 변경 되지 않았다.

> 알티베이스 샤딩 프로토콜 및 메타는 상위, 하위 호환성을 보장하지
> 않는다. 즉, 샤딩 버전이 다른 경우, 재구성해야 한다.

### 프로퍼티

#### 추가된 프로퍼티

#### 변경된 프로퍼티

#### 삭제된 프로퍼티

### 성능 뷰

#### 추가된 성능 뷰

#### 변경된 성능 뷰

#### 삭제된 성능 뷰
