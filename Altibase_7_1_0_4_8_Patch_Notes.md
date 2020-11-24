Altibase 7.1.0.4.7\~ Patch Notes
================================

New Features
------------

### BUG-46787 ACL에 허용되지 않은 접속이 있을 때 IP 정보를 출력해야 합니다.

-   **module** : mm

-   **Category** : Functionality

-   **재현 빈도** : Always

-   **증상** : access\_list 접근 제어시 에러 로그 메세지 변경

    \* 변경전

    ERR-410e9(errno=0) Connection is not permitted by the ACCESS\_LIST:
    0.0.0.0

    Dispatcher callback failed

    \* 변경후   

    ERR-410e9(errno=0) Connection is not permitted by the ACCESS\_LIST:
    0.0.0.0 **(CLIENT IP)**

    Dispatcher callback failed

-   **재현 방법**

    -   **재현 절차**

            # altibase.properties
            access_list = deny     ,0.0.0.0                 ,0.0.0.0
            $ is -s 192.168.XX.XX -port XXXXX

    -   **수행 결과**

            ERR-410e9(errno=0) Connection is not permitted by the ACCESS_LIST: 0.0.0.0Dispatcher callback failed                                                                      

    -   **예상 결과**

            ERR-410e9(errno=0) Connection is not permitted by the ACCESS_LIST: 0.0.0.0 (CLIENT IP)Dispatcher callback failed

-   **Workaround**

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

Fixed Bugs
----------

### BUG-48208 PSM 의 TIMESTAMP 제약을 제거합니다.

-   **module** : qp-psm-trigger-pvo

-   **Category** : Enhancement

-   **재현 빈도** : Always

-   **증상** : PSM 의 TIMESTAMP 제약 제거

-   **재현 방법**

    -   **재현 절차**

            drop trigger i3;
            drop table test_tri cascade;
            create table test_tri (c1 integer,c2 timestamp);
            alter system set __show_error_stack = 1;
            create trigger i3
            before insert on test_tri
            referencing new row new_row
            for each row
            as begin
            new_row.c2 := '2020100500' ;
            end;
            /

    -   **수행 결과**

            [ERR-31028 : Unable to create a column with the specified data type.
            In trigger SYS.I3
            0003 : referencing new row NEW_ROW
                                      ^      ^
            ]

    -   **예상 결과**

-   **Workaround**

        None.

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-48230 dequeue 성능 개선

-   **module** : sm

-   **Category** : Enhancement

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

### BUG-48234 Recursive with 구문의 JOIN이 NL 로 풀려서 성능이 하락됨.

-   **module** : qp-dml-execute

-   **Category** : Efficiency

-   **재현 빈도** : Always

-   **증상** : Recursive with 구문의 JOIN cost 조정

-   **재현 방법**

    -   **재현 절차**

            drop table PM_EQ_DTL;
            create table PM_EQ_DTL(
                COMPANY_CD  VARCHAR(28) FIXED,
                EQP_CD      VARCHAR(200) VARIABLE,
                VLID_TO_DT  VARCHAR(32) VARIABLE,
                VLID_FROM_DT VARCHAR(32) VARIABLE,
                EQP_TAB_NO_DC   VARCHAR(400) VARIABLE,
                PLANT_CD        VARCHAR(28) FIXED,
                PLAN_PLANT_CD   VARCHAR(28) FIXED,
                PLANGRP_CD      VARCHAR(28) FIXED,
                WC_CD           VARCHAR(28) FIXED,
                MAINT_WC_CD     VARCHAR(28) FIXED,
                WC_PLANT_CD     VARCHAR(28) FIXED,
                UP_EQP_CD       VARCHAR(28) FIXED
                );
            alter table PM_EQ_DTL add primary key ( COMPANY_CD, EQP_CD, VLID_TO_DT);
            insert into PM_EQ_DTL( COMPANY_CD, EQP_CD, VLID_TO_DT, UP_EQP_CD) select '1000', level, '99991231', NULL from dual connect by level < 16317;
            insert into PM_EQ_DTL( COMPANY_CD, EQP_CD, VLID_TO_DT, UP_EQP_CD) select '1000', level*100000, '99991231', level from dual connect by level < 143358;
            WITH CTE_LVL( COMPANY_CD, EQP_CD, LVL ) 
            AS
            (
                SELECT COMPANY_CD, EQP_CD, 6 LVL
                FROM PM_EQ_DTL
                WHERE COMPANY_CD = '1000'
                  AND VLID_TO_DT = '99991231'
                  AND UP_EQP_CD IS NULL
                UNION ALL
                SELECT A.COMPANY_CD, A.EQP_CD, B.LVL+1 LVL
                FROM PM_EQ_DTL A INNER JOIN CTE_LVL B ON B.COMPANY_CD = A.COMPANY_CD AND B.EQP_CD = A.UP_EQP_CD
                WHERE A.COMPANY_CD = '1000'
                AND A.VLID_TO_DT = '99991231'
                AND A.UP_EQP_CD IS NOT NULL
            )
            select count(*) from CTE_LVL;

    -   **수행 결과**

            Hang

    -   **예상 결과**

            COUNT(*)----------     32633

-   **Workaround**

        WITH CTE_LVL( COMPANY_CD, EQP_CD, LVL ) AS(    SELECT COMPANY_CD, EQP_CD, 6 LVL    FROM PM_EQ_DTL    WHERE COMPANY_CD = '1000'      AND VLID_TO_DT = '99991231'      AND UP_EQP_CD IS NULL    UNION ALL    SELECT /*+ USE_HASH( A, B ) */ A.COMPANY_CD, A.EQP_CD, B.LVL+1 LVL    FROM PM_EQ_DTL A INNER JOIN CTE_LVL B ON B.COMPANY_CD = A.COMPANY_CD AND B.EQP_CD = A.UP_EQP_CD    WHERE A.COMPANY_CD = '1000'    AND A.VLID_TO_DT = '99991231'    AND A.UP_EQP_CD IS NOT NULL)select count(*) from CTE_LVL;

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-48253 CLI처리중 SIGALRM 발생시 Hang이 발생

-   **module** : mm-cli

-   **Category** : Functionality

-   **재현 빈도** : Always

-   **증상** : 동일한 thread에서 mutex lock이 중복 시도되었을 경우 에러
    리턴 후 socket close.

    이 경우 사용자는 connection을 재 연결하여 사용해야 한다.

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
        -   153, HY010, ulERR\_ABORT\_LOCK\_SEQUENCE\_ERR = Lock
            sequence error.\
            \
            \# \*Cause: invalid Lock call sequence.\
            \
            \# \*Action: Try disconnect and reconnect 

### BUG-48273 Pivot에 사용된 Aggregaion이 상위 노드에 의해 쌓이는 경우 FATAL이 발생하는 경우가 있음

-   **module** : qp-select-execute

-   **Category** : Fatal

-   **재현 빈도** : Always

-   **증상** : Pivot에 사용된 Aggregaion이 상위 노드에 의해 쌓이는 경우
    FATAL이 발생 수정

-   **재현 방법**

    -   **재현 절차**

            drop table t14;
            create table t14 (
            RSLT_REPRT_PK                            NUMERIC(22),
            EVL_SCORE                                VARCHAR(5),
            CHKLIST_ITEM_PK                          NUMERIC(22)
            ) tablespace sys_tbs_disk_data;
            insert into t14 values( 205, '1', 135);
            insert into t14 values( 205, NULL, 1349);
            insert into t14 values( 205, NULL, 1340);
            insert into t14 values( 205, NULL, 1341);
            insert into t14 values( 205, '1', 134);
            insert into t14 values( 205, NULL, 1339);
            insert into t14 values( 205, NULL, 1330);
            insert into t14 values( 205, NULL, 1331);
            insert into t14 values( 205, '1', 133);
            insert into t14 values( 205, NULL, 1329);
            insert into t14 values( 205, NULL, 1320);
            insert into t14 values( 205, NULL, 1321);
            insert into t14 values( 205, '1', 132);
            insert into t14 values( 205, NULL, 1319);
            insert into t14 values( 205, NULL, 1310);
            insert into t14 values( 205, NULL, 1311);
            insert into t14 values( 205, '1', 131);
            insert into t14 values( 205, 'A', 13);
            insert into t14 values( 205, NULL, 1269);
            insert into t14 values( 205, NULL, 1260);
            drop table t24;
            create table t24 (
            RSLT_REPRT_PK                            NUMERIC(22),
            CHK_OPRTN_PK                             NUMERIC(22),
            LAST_TRSCT_STTUS_CD                      VARCHAR(2)
            ) tablespace sys_tbs_disk_data;
            insert into t24 values(196,         612,         '02');
            insert into t24 values(203,         683,         '02');
            insert into t24 values(205,         717,         '07');
            insert into t24 values(224,         726,         '03');
            insert into t24 values(232,         751,         '02');
            insert into t24 values(243,         808,         '02');
            insert into t24 values(251,         811,         '05');
            insert into t24 values(314,         1002,        '03');
            insert into t24 values(345,         937,         '02');
            insert into t24 values(347,         933,         '02');
            insert into t24 values(353,         820,         '02');
            insert into t24 values(356,         819,         '03');
            insert into t24 values(357,         999,         '02');
            insert into t24 values(363,         998,         '03');
            insert into t24 values(365,         959,         '02');
            insert into t24 values(386,         951,         '02');
            insert into t24 values(388,         994,         '02');
            insert into t24 values(182,         596,         '06');
            insert into t24 values(208,         729,         '08');
            insert into t24 values(247,         815,         '06');
            drop table t34;
            create table t34 (
            RSLT_REPRT_PK                            NUMERIC(22)
            ) tablespace sys_tbs_disk_data;
            insert into t34 values(196);
            insert into t34 values(203);
            insert into t34 values(205);
            insert into t34 values(205);
            insert into t34 values(205);
            insert into t34 values(224);
            select /*+ USE_HASH( t34, tt4 ) */ * from t34, (
            select /*+  */*
              from (select /*+  */a.RSLT_REPRT_PK,
                           a.CHKLIST_ITEM_PK,
                           a.EVL_SCORE,
                           b.CHK_OPRTN_PK
                      FROM t14 a ,
                           t24 b
                     where a.RSLT_REPRT_PK = b.RSLT_REPRT_PK
                       and b.LAST_TRSCT_STTUS_CD = '07'
                        )
            pivot ( max(EVL_SCORE) for CHKLIST_ITEM_PK in (
            11   ,111  ,112  ,113  ,114  ,115  ,12   ,124  ,121  ,122  ,123  ,125  ,126  ,13   ,134  ,136  ,135  ,133  ,132  ,131,
            22   ,221  ,222  ,223  ,23   ,233  ,234  ,231  ,232  ,21   ,211  ,212  ,
            32   ,321  ,322  ,31   ,311  ,41   ,411  ,414  ,413  ,412  ,42   ,424  ,421  ,423  ,422  ,43   ,431 ,
            52   ,521  ,522  ,523  ,53   ,533  ,534  ,532  ,531  ,51   ,511  ,512  ,513 ))) tt4
            where t34.RSLT_REPRT_PK = tt4.RSLT_REPRT_PK
            ;

    -   **수행 결과**

            FATAL

    -   **예상 결과**

            NOT FATAL

-   **Workaround**

        /*+ USE_HASH( tt4, t34  ) */

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-48287 REPLICATION\_SYNC\_LOG이 1일때 Offline replication을 하면 읽어온 로그를 Sender가 보낼수 없습니다.

-   **module** : rp

-   **Category** : Functional Error

-   **재현 빈도** : Always

-   **증상** : REPLICATION\_SYNC\_LOG 프로퍼티를 1로 설정하면 송신
    쓰레드는 디스크에 내려간 로그만 보내게 되는데 Offline replication
    에서는 디스크에 내려가도록 기다릴 필요가 없는데, 디스크로 내려가는걸
    기다리는 루틴을 다고 있으서 문제가 발생하였습니다.

    Offline replication 일때는 REPLICATION\_SYNC\_LOG 프로퍼티를
    적용받지 않도록 수정하였습니다.

-   **재현 방법**

    -   **재현 절차**

            REPLICATION_SYNC_LOG = 1
            Standby 서버에서 Offline replication 수행

    -   **수행 결과**

            Offline replication 가 끝나지 않음

    -   **예상 결과**

            Offline replication 가 정상적으로 완료

-   **Workaround**

        REPLICATION_SYNC_LOG 를 0으로 설정한다.

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
