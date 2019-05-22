<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Altibase 7.1.0.1.7 Patch Notes](#altibase-71017-patch-notes)
  - [New Features](#new-features)
    - [BUG-46418 호스트 변수 데이터 타입 APRE\_BINARY2를 지원해야 합니다.](#bug-46418%C2%A0%ED%98%B8%EC%8A%A4%ED%8A%B8-%EB%B3%80%EC%88%98-%EB%8D%B0%EC%9D%B4%ED%84%B0-%ED%83%80%EC%9E%85-apre%5C_binary2%EB%A5%BC-%EC%A7%80%EC%9B%90%ED%95%B4%EC%95%BC-%ED%95%A9%EB%8B%88%EB%8B%A4)
  - [Fixed Bugs](#fixed-bugs)
    - [BUG-46519 메모리 부족인 상황에서 메모리 할당 실패시 예외처리에서, 할당되지 않은 메모리를 해제하는 경우 비정상 종료하는 문제를 수정하였습니다.](#bug-46519%C2%A0%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%B6%80%EC%A1%B1%EC%9D%B8-%EC%83%81%ED%99%A9%EC%97%90%EC%84%9C-%EB%A9%94%EB%AA%A8%EB%A6%AC-%ED%95%A0%EB%8B%B9-%EC%8B%A4%ED%8C%A8%EC%8B%9C-%EC%98%88%EC%99%B8%EC%B2%98%EB%A6%AC%EC%97%90%EC%84%9C-%ED%95%A0%EB%8B%B9%EB%90%98%EC%A7%80-%EC%95%8A%EC%9D%80-%EB%A9%94%EB%AA%A8%EB%A6%AC%EB%A5%BC-%ED%95%B4%EC%A0%9C%ED%95%98%EB%8A%94-%EA%B2%BD%EC%9A%B0-%EB%B9%84%EC%A0%95%EC%83%81-%EC%A2%85%EB%A3%8C%ED%95%98%EB%8A%94-%EB%AC%B8%EC%A0%9C%EB%A5%BC-%EC%88%98%EC%A0%95%ED%95%98%EC%98%80%EC%8A%B5%EB%8B%88%EB%8B%A4)
    - [BUG-46526 aix grep에 -m 옵션이 없는데 사용하는 코드가 있어서 isql시 에러메시지가 발생.](#bug-46526%C2%A0aix-grep%EC%97%90--m-%EC%98%B5%EC%85%98%EC%9D%B4-%EC%97%86%EB%8A%94%EB%8D%B0-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94-%EC%BD%94%EB%93%9C%EA%B0%80-%EC%9E%88%EC%96%B4%EC%84%9C-isql%EC%8B%9C-%EC%97%90%EB%9F%AC%EB%A9%94%EC%8B%9C%EC%A7%80%EA%B0%80-%EB%B0%9C%EC%83%9D)
  - [Changes](#changes)
    - [Version Info](#version-info)
    - [호환성](#%ED%98%B8%ED%99%98%EC%84%B1)
    - [프로퍼티](#%ED%94%84%EB%A1%9C%ED%8D%BC%ED%8B%B0)
    - [성능 뷰](#%EC%84%B1%EB%8A%A5-%EB%B7%B0)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

Altibase 7.1.0.1.7 Patch Notes
==============================
New Features
------------

### BUG-46418 호스트 변수 데이터 타입 APRE\_BINARY2를 지원

- **module** : mm-apre

- **Category** : Efficiency

- **재현 빈도** : Always

- **증상** : BLOB insert의 성능 개선을 위해 호스트 변수 타입
  [APRE\_BINARY2](<https://github.com/ALTIBASE/Documents/blob/13554fc3e4451721db8a50f08fbabce281dcb5b5/Manuals/Altibase_7.1/kor/Precompiler_1.md#apre_binary2>)를 추가하였습니다. 128KB 이하의 작은 LOB 데이터를 Insert 할 때 유용합니다. 

- **재현 방법**

  -   **재현 절차**

          CREATE TABLE T1 (C1 BLOB)
          APRE_BINARY v_val[N];
          EXEC SQL INSERT INTO T1 VALUES(:v_val :blob_ind);

  -   **수행 결과**

          binding as SQL_BLOB

  -   **예상 결과**

          binding as SQL_BINARY

- **Workaround**

- **변경사항**

  -   Performance view
  -   Property
  -   Compile Option
  -   Error Code

Fixed Bugs
----------

### BUG-46519 메모리 부족인 상황에서 메모리 할당 실패시 예외처리에서, 할당되지 않은 메모리를 해제하는 경우 비정상 종료하는 문제를 수정하였습니다.

-   **module** : id

-   **Category** : Fatal

-   **재현 빈도** : Rare

-   **증상** : 메모리 풀에서 초기화과정에서 메모리가 부족할때 예외처리를
    하다가, 할당되지 않은 메모리를 해제하는 경우 비정상 종료 할 수 있는
    문제를 수정하였습니다.

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

### BUG-46526 AIX에서 iSQL 접속 시, "grep: Not a recognized flag: m" 에러 메시지 발생

- **module** : id

- **Category** : Functionality

- **재현 빈도** : Always

- **증상** : 내부 코드에서 aix에서 사용할수 없는 명령어(grep 명령어의
  -m 옵션)가 사용되고 있어, isql 수행시 에러메시지가 발생합니다. 이를
  수정하였습니다.

- **재현 방법**

  - **재현 절차**

    ```
    $ is
    -----------------------------------------------------------------
         Altibase Client Query utility.
         Release Version 7.1.0.1.2
         Copyright 2000, ALTIBASE Corporation or its subsidiaries.
         All Rights Reserved.
    -----------------------------------------------------------------
    grep: Not a recognized flag: m
    Usage: grep [-r] [-R] [-H] [-L] [-E|-F] [-c|-l|-q] [-insvxbhwyu] [-p[parasep]] -e pattern_list...
            [-f pattern_file...] [file...]
    Usage: grep [-r] [-R] [-H] [-L]  [-E|-F] [-c|-l|-q] [-insvxbhwyu] [-p[parasep]] [-e pattern_list...]
            -f pattern_file... [file...]
    Usage: grep [-r] [-R] [-H] [-L] [-E|-F] [-c|-l|-q] [-insvxbhwyu] [-p[parasep]] pattern_list [file...]
    grep: Not a recognized flag: m
    Usage: grep [-r] [-R] [-H] [-L] [-E|-F] [-c|-l|-q] [-insvxbhwyu] [-p[parasep]] -e pattern_list...
            [-f pattern_file...] [file...]
    Usage: grep [-r] [-R] [-H] [-L]  [-E|-F] [-c|-l|-q] [-insvxbhwyu] [-p[parasep]] [-e pattern_list...]
            -f pattern_file... [file...]
    Usage: grep [-r] [-R] [-H] [-L] [-E|-F] [-c|-l|-q] [-insvxbhwyu] [-p[parasep]] pattern_list [file...]
    ISQL_CONNECTION = TCP, SERVER = localhost, PORT_NO = 20300
    iSQL> exit
    ```

  - **수행 결과**

  - **예상 결과**

- **Workaround**

- **변경사항**

  -   Performance view
  -   Property
  -   Compile Option
  -   Error Code

Changes
-------

### Version Info

  altibase version   database binary version   meta version   cm protocol version   replication protocol version   sharding version
------------------ ------------------------- -------------- --------------------- ------------------------------ ------------------
  7.1.0.1.7          6.5.1                     8.6.1          7.1.6                 7.4.3                          2.1.0

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

추가/변경/삭제된 프로퍼티 없음

### 성능 뷰

추가/변경/삭제된 프로퍼티 없음