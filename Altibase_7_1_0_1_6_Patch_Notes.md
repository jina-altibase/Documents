Altibase 7.1.0.1.6 Patch Notes
==============================

New Features
------------

### BUG-46402 메모리 인덱스에 할당된 메모리는 mempool로 반환되지 않습니다.

-   **module** : sm-mem-index

-   **Category** : Efficiency

-   **재현 빈도** : Always

-   **증상** : 메모리 인덱스에 할당된 메모리는 영원히 free되지 않고
    재사용만 가능했습니다.

    이부분을 실제 free가 이루어지도록 수정하였습니다.

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

### BUG-46406 merge 구문에 syntax 확장

-   **module** : qp-dml-pvo

-   **Category** : Other

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

### BUG-46436 모니터링 API의 ABISqlText에 time 항목을 추가해야 합니다.

-   **module** : mm-altibaseMonitor

-   **Category** : Functionality

-   **재현 빈도** : Always

-   **증상** : altibaseMonitor의 ABISqlText에 아래 필드 추가.

    PARSE\_TIME                          파싱 소요 시간

    SOFT\_PREPARE\_TIME            Prepare 과정중 SQL Plan Cache에서
    plan 탐색 시간

    LAST\_QUERY\_START\_TIME    가장 최근의 쿼리 시작 시간

    EXECUTE\_TIME                     실행 소요 시간

    FETCH\_TIME                         Fetch 소요 시간

    FETCH\_START\_TIME              현재 Fetch 시작 시간

    TOTAL\_TIME                         총 경과 시간

    VALIDATE\_TIME                     정당성 검사 소요 시간

    OPTIMIZE\_TIME                    최적화 소요 시간

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

### BUG-46480 JDBC insert 성능개선을 위한 내부 함수 리펙토링

-   **module** : mm-jdbc

-   **Category** : Efficiency

-   **재현 빈도** : Always

-   **증상** : JDBC insert 성능개선을 위한 내부 함수 리펙토링

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

### BUG-46481 micro second sleep 을 지원하는 시스템 저장 프로시저 sleep2가 추가되었습니다.

-   **module** : qx

-   **Category** : Enhancement

-   **재현 빈도** : Always

-   **증상** : dbms\_lock 패키지에 micro second sleep 을 지원하는 시스템
    저장 프로시저 sleep2가 추가되었습니다.

    구문

    DBMS\_LOCK.SLEEP2(seconds IN INTEGER, microseconds IN INTEGER );

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

### BUG-46485 성능개선을 위해 double 데이터의 바인딩 타입을 SQL\_C\_DOUBLE에서 SQL\_C\_CHAR로 수정해야 합니다

-   **module** : ux-iloader

-   **Category** : Efficiency

-   **재현 빈도** : Always

-   **증상** : iloade 내부적으로 double 타입을 처리할 때 파라미터 바인딩
    타입을 변경함으로써 IN 성능 개선 (사용자 인터페이스 변경 없음)

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

### BUG-46486 성능 개선을 위해, 버퍼로부터 데이터를 읽을 때 레코드 단위가 아니라 array 단위로 락을 획득하도록 수정해야 합니다

-   **module** : ux-iloader

-   **Category** : Efficiency

-   **재현 빈도** : Always

-   **증상** : IN 수행 시 작업 스레드들이 버퍼에서 데이터를 읽어갈 때 락
    획득 단위를 변경함으로써 성능 개선

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

Fixed Bugs
----------

### BUG-46085 캐싱된 플랜을 확인하는 과정에서 할당된 Query\_Prepare 메모리를 해제하지 않습니다.

-   **module** : qp-select-pvo

-   **Category** : Memory Error

-   **재현 빈도** : Always

-   **증상** : 캐싱된 플랜을 확인하는 과정에서 할당된 Query\_Prepare
    메모리를 해제하지 않습니다.

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

### BUG-46389 APRE usage 에 silent 옵션이 누락되었습니다.

-   **module** : mm-apre

-   **Category** : Maintainability

-   **재현 빈도** : Always

-   **증상** : APRE -h 출력에 silent 옵션과 설명을 추가하였습니다.

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

### BUG-46390 IPCDA Session 종료시 Semaphore를 통한 Client APP 생존여부 체크 로직이 누락되어 있습니다.

-   **module** : mm

-   **Category** : Memory Error

-   **재현 빈도** : Frequence

-   **증상** : IPCDA Session 종료시 Client APP Check 로직 추가.

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

### BUG-46483 HP jdbcAdapter 에서 LD\_LIBRARY\_PATH를 설정하지 않아도 oaUtility start 수행시 에러가 발생하지 않습니다.

-   **module** : rp-jdbcAdapter

-   **Category** : Maintainability

-   **재현 빈도** : Always

-   **증상** : HP 장비에서 LD\_LIBRARY\_PATH에 libjvm.so Path가 설정
    되어 있지 않으면 에러가 발생하도록 수정

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

### BUG-46508 min, max 통계 정보 설정 시 테이블 메타 캐시의 컬럼 정보가 변경될 수 있습니다.

-   **module** : qp-meta

-   **Category** : Fatal

-   **재현 빈도** : Always

-   **증상** : min, max 통계 정보 설정 시 테이블 메타 캐시의 컬럼 정보가
    변경될 수 있습니다.

-   **재현 방법**

    -   **재현 절차**

            create table t1 ( c1 varchar(10) ) tablespace sys_tbs_disk_data;
            insert into t1 select level from dual connect by level <= 10000;
            exec set_column_stats('sys', 't1', 'c1', NULL, 9995, 0, 5, '1111111111', '9999999999');
            select /*+ no_merge(a) */ count(*) from (select * from t1) a;
            exec set_column_stats('sys', 't1', 'c1', NULL, 9995, 0, 5, '1', '9999');
            select /*+ no_merge(a) */ count(*) from (select * from t1) a;

    -   **수행 결과**

            iSQL> exec set_column_stats('sys', 't1', 'c1', NULL, 9995, 0, 5, '1', '9999');
            Execute success.
            iSQL> select /*+ no_merge(a) */ count(*) from (select * from t1) a;
            [ERR-91015 : Communication failure.]

    -   **예상 결과**

            iSQL> exec set_column_stats('sys', 't1', 'c1', NULL, 9995, 0, 5, '1', '9999');
            Execute success.
            iSQL> select /*+ no_merge(a) */ count(*) from (select * from t1) a;
            COUNT(*)             
            -----------------------
            10000                
            1 row selected.

-   **Workaround**

        iSQL> exec set_column_stats('sys', 't1', 'c1', NULL, 9995, 0, 5);
        Execute success.
        iSQL> select /*+ no_merge(a) */ count(*) from (select * from t1) a;
        COUNT(*)             
        -----------------------
        10000                
        1 row selected.

-   **변경사항**

    -   Performance view
    -   Property
    -   Compile Option
    -   Error Code

### BUG-46516 APRE PSM Array가 새로 생성된 User에서 동작하지 않습니다.

-   **module** : mm-apre

-   **Category** : Functional Error

-   **재현 빈도** : Always

-   **증상** : PSM Array 로직에서 조회하는 metatable을
    SYSTEM\_.DBA\_USERS\_ -\> SYSTEM\_.SYS\_USERS\_ 로 변경

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
