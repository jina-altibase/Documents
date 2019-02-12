<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Altibase 7.1.0.1.8 Patch Notes](#altibase-71018-patch-notes)
  - [New Features](#new-features)
    - [BUG-46174 저장 프로시저내 insert, update 구문에서 레코드 타입변수 사용하도록 기능 확장](#bug-46174저장-프로시저내-insert-update-구문에서-레코드-타입변수-사용하도록-기능-확장)
  - [Fixed Bugs](#fixed-bugs)
    - [BUG-46120 Active Server와 Standby Server의 해시 파티션드 테이블의 파티션 개수가 다른 경우, 이중화가 실패해야 합니다.](#bug-46120active-server와-standby-server의-해시-파티션드-테이블의-파티션-개수가-다른-경우-이중화가-실패해야-합니다)
    - [BUG-46396 aexport가 생성하는 DDL 마지막 라인에 덧붙이는 newline으로 인해 iSQL에서 Syntax Error가 발생할 수 있습니다.](#bug-46396aexport가-생성하는-ddl-마지막-라인에-덧붙이는-newline으로-인해-isql에서-syntax-error가-발생할-수-있습니다)
    - [BUG-46515 dumptrc을 사용해서 콜스택 출력시 altibase_error.log의 콜스택이 생략되는 경우가 있어, 이를 수정하였습니다.](#bug-46515dumptrc을-사용해서-콜스택-출력시-altibase_errorlog의-콜스택이-생략되는-경우가-있어-이를-수정하였습니다)
    - [BUG-46539 merge 구문에 parser conflicts 발생](#bug-46539merge-구문에-parser-conflicts-발생)
    - [BUG-46550 JDBC 드라이버에서 addBatch시에 directByteBuffer 사용시 메모리 증가하는 문제가 있습니다.](#bug-46550jdbc-드라이버에서-addbatch시에-directbytebuffer-사용시-메모리-증가하는-문제가-있습니다)
    - [BUG-46551  jdbcAdapter로 altibase 5.5.1 에 데이터 전송시 ArrayIndexOutOfBoundsException 이 발생하는 경우가 있습니다.](#bug-46551-jdbcadapter로-altibase-551-에-데이터-전송시-arrayindexoutofboundsexception-이-발생하는-경우가-있습니다)
    - [BUG-46552 isql에서 /dev/null을 사용하지 않아야 합니다](#bug-46552isql에서-devnull을-사용하지-않아야-합니다)
    - [BUG-46567 dumpStack의 mCallStackCriticalSection에 동시성문제 있음.](#bug-46567dumpstack의-mcallstackcriticalsection에-동시성문제-있음)
    - [BUG-46572 APRE에서 packge를 사용시 psm array가 제대로 인식되지 않습니다.](#bug-46572apre에서-packge를-사용시-psm-array가-제대로-인식되지-않습니다)
    - [BUG-46574 Checkpoint Image 생성 도중에 서버가 비정상 종료되면 재구동에 실패 합니다.](#bug-46574checkpoint-image-생성-도중에-서버가-비정상-종료되면-재구동에-실패-합니다)
    - [BUG-46586 Diag Record 관련 함수는 Function Context 의 Object 를 사용해야 합니다.](#bug-46586diag-record-관련-함수는-function-context-의-object-를-사용해야-합니다)
    - [BUG-46598 V$REPGAP 퍼포먼스뷰의 REP_GAP 컬럼을 size 단위로 변경합니다.](#bug-46598vrepgap-퍼포먼스뷰의-rep_gap-컬럼을-size-단위로-변경합니다)
    - [BUG-46600 APRE PSM Array에서 User.Package.Procedure의 형태도 인식가능해야 합니다.](#bug-46600apre-psm-array에서-userpackageprocedure의-형태도-인식가능해야-합니다)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Altibase 7.1.0.1.8 Patch Notes

## New Features

<h3>BUG-46174&nbsp;저장 프로시저내 insert, update 구문에서 레코드 타입변수 사용하도록 기능 확장</h3>
<table width="100%">
<tbody>
<tr>
<td colspan="2" width="189">
<p><strong>Module</strong></p>
</td>
<td width="378">
<p>qp-psm-trigger-execute</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Category</strong></p>
</td>
<td width="378">
<p>Functionality</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>재현빈도</strong></p>
</td>
<td width="378">
<p>Always</p>
</td>
</tr>
<tr>
<td rowspan="3" width="86">
<p><strong>Reproducing Conditions</strong></p>
</td>
<td width="109">
<p><strong>재현절차</strong></p>
</td>
<td width="378">
<p>create table t1( c1 int, c2 int );<br /> insert into t1 values( 0, 0);<br /> create or replace procedure proc1 as<br /> type tr is record ( c1 int, c2 int );<br /> var tr;<br /> begin<br /> var.c1 := 1;<br /> var.c2 :=2;<br /> update t1 set row = var;<br /> var.c1 := 3;<br /> var.c2 :=4;<br /> insert into t1 values var;<br /> end;<br /> /<br /> exec proc1;<br /> select * from t1;</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>수행결과</strong></p>
</td>
<td width="378">
<p>[ERR-31001 : SQL syntax error</p>
<p>&nbsp;</p>
<p>line 7: missing or invalid syntax</p>
<p>update T1 set row = var;</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ^ ^</p>
<p>&nbsp;</p>
<p>]</p>
<p>iSQL&gt; exec proc1;</p>
<p>[ERR-31129 : Procedure or function not found :</p>
<p>0001 : exec PROC1</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ^&nbsp;&nbsp;&nbsp; ^</p>
<p>.]</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>예상결과</strong></p>
</td>
<td width="378">
<p>exec proc1;<br /> Execute success.<br /> select * from t1;<br /> C1 C2 <br /> ---------------------------<br /> 1 2 <br /> 3 4 <br /> 2 rows selected.</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>증상</strong></p>
</td>
<td width="378">
<p>저장 프로시저 내에서 insert update 구문에서도 레코드타입 변수를 사용할수 있도록 합니다.<br /> 이때, 레코드 변수의 칼럼의 개수와 명시한 테이블의 칼럼의 개수가 동일해야 합니다. 또한 레코드 타입 내부에 정의한 칼럼은 명시한 테이블 칼럼의 타입과 순서대로 정확히 일치하거나 호환이 가능해야 합니다. 만약 테이블의 칼럼에 NOT NULL 제약조건이 있으면 대응되는 레코드의 칼럼에 NULL 값을 사용할 수 없습니다.&nbsp;&nbsp;</p>
</td>
</tr>
<tr>
<td rowspan="4" width="86">
<p><strong>변경사항</strong></p>
</td>
<td width="109">
<p><strong>Performance View</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Property</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Compile Option</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Error Code</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Workaround</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
</tbody>
</table>

## Fixed Bugs

<h3><br />BUG-46120&nbsp;Active Server와 Standby Server의 해시 파티션드 테이블의 파티션 개수가 다른 경우, 이중화가 실패해야 합니다.</h3>
<table width="100%">
<tbody>
<tr>
<td colspan="2" width="189">
<p><strong>Module</strong></p>
</td>
<td width="378">
<p>rp</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Category</strong></p>
</td>
<td width="378">
<p>Functional Error</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>재현빈도</strong></p>
</td>
<td width="378">
<p>Always</p>
</td>
</tr>
<tr>
<td rowspan="3" width="86">
<p><strong>Reproducing Conditions</strong></p>
</td>
<td width="109">
<p><strong>재현절차</strong></p>
</td>
<td width="378">
<p>-- Active<br /> CREATE TABLE T1<br /> (<br /> C1 INTEGER PRIMARY KEY,<br /> C2 INTEGER<br /> )<br /> PARTITION BY HASH( C1 )<br /> (<br /> PARTITION P1,<br /> PARTITION P2<br /> );<br /> -- Standby <br /> CREATE TABLE T1<br /> (<br /> C1 INTEGER PRIMARY KEY,<br /> C2 INTEGER<br /> )<br /> PARTITION BY HASH( C1 )<br /> (<br /> PARTITION P1,<br /> PARTITION P2,<br /> PARTITION P3<br /> );<br /> CREATE REPLICATION REP1<br /> WITH '${HOST_IP@DB1}', ${ALTIBASE_REPLICATION_PORT_NO@DB1}<br /> FROM SYS.T1 PARTITION P2 TO SYS.T1 PARTITION P2;<br /> -- Active 에서<br /> ALTER REPLICATION REP1 START;</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>수행결과</strong></p>
</td>
<td width="378">
<p>$T1&gt; ALTER REPLICATION REP1 START;<br /> Alter success.</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>예상결과</strong></p>
</td>
<td width="378">
<p>$T1&gt; ALTER REPLICATION REP1 START;<br /> Fail..</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>증상</strong></p>
</td>
<td width="378">
<p>Active Server와 Standby Server의 해시 파티션드 테이블의 파티션 개수가 다른 경우, 이중화 실패 에러가 발생하도록 수정하였습니다. 이로 인해 replication protocol version이 7.4.3 에서 7.4.4 로 변경되었습니다.&nbsp;&nbsp;</p>
</td>
</tr>
<tr>
<td rowspan="4" width="86">
<p><strong>변경사항</strong></p>
</td>
<td width="109">
<p><strong>Performance View</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Property</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Compile Option</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Error Code</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Workaround</strong></p>
</td>
<td width="378">
<p>...</p>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<h3>BUG-46396&nbsp;aexport가 생성하는 DDL 마지막 라인에 덧붙이는 newline으로 인해 iSQL에서 Syntax Error가 발생할 수 있습니다.</h3>
<table width="100%">
<tbody>
<tr>
<td colspan="2" width="189">
<p><strong>Module</strong></p>
</td>
<td width="378">
<p>ux-aexport</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Category</strong></p>
</td>
<td width="378">
<p>Enhancement</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>재현빈도</strong></p>
</td>
<td width="378">
<p>Always</p>
</td>
</tr>
<tr>
<td rowspan="3" width="86">
<p><strong>Reproducing Conditions</strong></p>
</td>
<td width="109">
<p><strong>재현절차</strong></p>
</td>
<td width="378">
<p>iSQL&gt; CREATE VIEW "V1" AS SELECT SYSDATE FROM dual<br /> 2<br /> iSQL&gt; ;<br /> [ERR-91010 : Syntax Error]</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>수행결과</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>예상결과</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>증상</strong></p>
</td>
<td width="378">
<p>aexport가 생성하는 PSM(procedure, function, view) DDL의 끝 부분 공백 라인으로 인해 iSQL 프롬프트 상에서 수행 시 에러가 발생할 수 있어, 이를 수정하였습니다.&nbsp;&nbsp;</p>
</td>
</tr>
<tr>
<td rowspan="4" width="86">
<p><strong>변경사항</strong></p>
</td>
<td width="109">
<p><strong>Performance View</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Property</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Compile Option</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Error Code</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Workaround</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<h3>BUG-46515&nbsp;dumptrc을 사용해서 콜스택 출력시 altibase_error.log의 콜스택이 생략되는 경우가 있어, 이를 수정하였습니다.</h3>
<table width="100%">
<tbody>
<tr>
<td colspan="2" width="189">
<p><strong>Module</strong></p>
</td>
<td width="378">
<p>id</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Category</strong></p>
</td>
<td width="378">
<p>Enhancement</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>재현빈도</strong></p>
</td>
<td width="378">
<p>Rare</p>
</td>
</tr>
<tr>
<td rowspan="3" width="86">
<p><strong>Reproducing Conditions</strong></p>
</td>
<td width="109">
<p><strong>재현절차</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>수행결과</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>예상결과</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>증상</strong></p>
</td>
<td width="378">
<p>dumptrc을 사용해서 콜스택 출력시&nbsp;문자열파싱에 오류가 있었습니다. 이로 인해&nbsp;altibase_error.log의 콜스택이&nbsp;생략되는 경우가 발생하여 이를 수정합니다.&nbsp;&nbsp;</p>
</td>
</tr>
<tr>
<td rowspan="4" width="86">
<p><strong>변경사항</strong></p>
</td>
<td width="109">
<p><strong>Performance View</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Property</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Compile Option</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Error Code</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Workaround</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<h3>BUG-46539&nbsp;merge 구문에 parser conflicts 발생</h3>
<table width="100%">
<tbody>
<tr>
<td colspan="2" width="189">
<p><strong>Module</strong></p>
</td>
<td width="378">
<p>qp-ddl-dcl-pvo</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Category</strong></p>
</td>
<td width="378">
<p>Other</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>재현빈도</strong></p>
</td>
<td width="378">
<p>Always</p>
</td>
</tr>
<tr>
<td rowspan="3" width="86">
<p><strong>Reproducing Conditions</strong></p>
</td>
<td width="109">
<p><strong>재현절차</strong></p>
</td>
<td width="378">
<p>drop table t1;<br /> drop table t2;<br /> create table t1( i1 integer, i2 integer );<br /> insert into t1 values (1, 100);<br /> insert into t1 values (2, 100);<br /> insert into t1 values (2, 200);<br /> insert into t1 values (3, 100);<br /> insert into t1 values (3, 300);<br /> insert into t1 values (4, 400);<br /> create table t2( i1 integer, i2 integer );<br /> insert into t2 values (1, 1);<br /> insert into t2 values (2, 2);<br /> insert into t2 values (3, 3);<br /> insert into t2 values (6, null);<br /> merge into t1 using t2 on (t1.i1 = t2.i1) and (t1.i1 = t2.i1)<br /> when matched then <br /> update set t1.i2 = t1.i2+t2.i2;</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>수행결과</strong></p>
</td>
<td width="378">
<p>iSQL&gt; merge into t1 using t2 on (t1.i1 = t2.i1) and (t1.i1 = t2.i1)<br /> 2 when matched then<br /> 3 update set t1.i2 = t1.i2+t2.i2;<br /> [ERR-31001 : SQL syntax error<br /> line 1: missing or invalid syntax<br /> merge into T1 using T2 on (T1.I1 = T2.I1) and (t1.i1 = t2.i1)<br /> ^ ^<br /> ]</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>예상결과</strong></p>
</td>
<td width="378">
<p>iSQL&gt; merge into t1 using t2 on (t1.i1 = t2.i1) and (t1.i1 = t2.i1)<br /> 2 when matched then<br /> 3 update set t1.i2 = t1.i2+t2.i2;<br /> 5 rows merged.</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>증상</strong></p>
</td>
<td width="378">
<p>merge query에서 ON clause의 parsing rule 변경&nbsp;&nbsp;</p>
</td>
</tr>
<tr>
<td rowspan="4" width="86">
<p><strong>변경사항</strong></p>
</td>
<td width="109">
<p><strong>Performance View</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Property</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Compile Option</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Error Code</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Workaround</strong></p>
</td>
<td width="378">
<p>merge into t1 using t2 on ((t1.i1 = t2.i1) and (t1.i1 = t2.i1))<br /> when matched then <br /> update set t1.i2 = t1.i2+t2.i2;</p>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<h3>BUG-46550&nbsp;JDBC 드라이버에서 addBatch시에 directByteBuffer 사용시 메모리 증가하는 문제가 있습니다.</h3>
<table width="100%">
<tbody>
<tr>
<td colspan="2" width="189">
<p><strong>Module</strong></p>
</td>
<td width="378">
<p>mm-jdbc</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Category</strong></p>
</td>
<td width="378">
<p>Memory Error</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>재현빈도</strong></p>
</td>
<td width="378">
<p>Frequence</p>
</td>
</tr>
<tr>
<td rowspan="3" width="86">
<p><strong>Reproducing Conditions</strong></p>
</td>
<td width="109">
<p><strong>재현절차</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>수행결과</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>예상결과</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>증상</strong></p>
</td>
<td width="378">
<p>addBatch()시 사용하는 버퍼를 allocate() 메소드를 이용해 JAVA heap 영역에서 할당하도록 수정하였습니다.&nbsp;&nbsp;</p>
</td>
</tr>
<tr>
<td rowspan="4" width="86">
<p><strong>변경사항</strong></p>
</td>
<td width="109">
<p><strong>Performance View</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Property</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Compile Option</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Error Code</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Workaround</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<h3>BUG-46551&nbsp; jdbcAdapter로 altibase 5.5.1 에 데이터 전송시 ArrayIndexOutOfBoundsException 이 발생하는 경우가 있습니다.</h3>
<table width="100%">
<tbody>
<tr>
<td colspan="2" width="189">
<p><strong>Module</strong></p>
</td>
<td width="378">
<p>rp-jdbcAdapter</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Category</strong></p>
</td>
<td width="378">
<p>Other</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>재현빈도</strong></p>
</td>
<td width="378">
<p>Always</p>
</td>
</tr>
<tr>
<td rowspan="3" width="86">
<p><strong>Reproducing Conditions</strong></p>
</td>
<td width="109">
<p><strong>재현절차</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>수행결과</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>예상결과</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>증상</strong></p>
</td>
<td width="378">
<p>&nbsp;jdbcAdapter로&nbsp;데이터 전송 batch 작업 진행&nbsp;시 에러가 발생하면, jdbc driver에서 자체적으로 에러가 발생한 batch 작업을 정리하는데, Altibase 6.1.1 이하의 경우 jdbc driver가 자체적으로 정리하는 기능이 없어 ArrayIndexOutOfBoundException이 발생합니다.<br /> jdbc driver 수정하는 작업은 호환성 이슈가 있어 수정하지 않습니다. 이에, jdbcAdapter 에서&nbsp;내부적으로 배치작업을 정리할 수 있도록 수정하였습니다.&nbsp;&nbsp;</p>
</td>
</tr>
<tr>
<td rowspan="4" width="86">
<p><strong>변경사항</strong></p>
</td>
<td width="109">
<p><strong>Performance View</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Property</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Compile Option</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Error Code</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Workaround</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<h3>BUG-46552&nbsp;isql에서 /dev/null을 사용하지 않아야 합니다</h3>
<table width="100%">
<tbody>
<tr>
<td colspan="2" width="189">
<p><strong>Module</strong></p>
</td>
<td width="378">
<p>ux-isql</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Category</strong></p>
</td>
<td width="378">
<p>Other</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>재현빈도</strong></p>
</td>
<td width="378">
<p>Always</p>
</td>
</tr>
<tr>
<td rowspan="3" width="86">
<p><strong>Reproducing Conditions</strong></p>
</td>
<td width="109">
<p><strong>재현절차</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>수행결과</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>예상결과</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>증상</strong></p>
</td>
<td width="378">
<p>ISQL_HIST_FILE 환경변수가 설정되어 있지 않은 경우&nbsp;/dev/null로 출력하던 것을 아예 출력하지 않도록 수정함&nbsp;&nbsp;</p>
</td>
</tr>
<tr>
<td rowspan="4" width="86">
<p><strong>변경사항</strong></p>
</td>
<td width="109">
<p><strong>Performance View</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Property</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Compile Option</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Error Code</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Workaround</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<h3>BUG-46567&nbsp;dumpStack의 mCallStackCriticalSection에 동시성문제 있음.</h3>
<table width="100%">
<tbody>
<tr>
<td colspan="2" width="189">
<p><strong>Module</strong></p>
</td>
<td width="378">
<p>id</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Category</strong></p>
</td>
<td width="378">
<p>Reliability</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>재현빈도</strong></p>
</td>
<td width="378">
<p>Rare</p>
</td>
</tr>
<tr>
<td rowspan="3" width="86">
<p><strong>Reproducing Conditions</strong></p>
</td>
<td width="109">
<p><strong>재현절차</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>수행결과</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>예상결과</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>증상</strong></p>
</td>
<td width="378">
<p>&nbsp;&nbsp;</p>
</td>
</tr>
<tr>
<td rowspan="4" width="86">
<p><strong>변경사항</strong></p>
</td>
<td width="109">
<p><strong>Performance View</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Property</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Compile Option</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Error Code</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Workaround</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<h3>BUG-46572&nbsp;APRE에서 packge를 사용시 psm array가 제대로 인식되지 않습니다.</h3>
<table width="100%">
<tbody>
<tr>
<td colspan="2" width="189">
<p><strong>Module</strong></p>
</td>
<td width="378">
<p>mm-apre</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Category</strong></p>
</td>
<td width="378">
<p>Functional Error</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>재현빈도</strong></p>
</td>
<td width="378">
<p>Always</p>
</td>
</tr>
<tr>
<td rowspan="3" width="86">
<p><strong>Reproducing Conditions</strong></p>
</td>
<td width="109">
<p><strong>재현절차</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>수행결과</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>예상결과</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>증상</strong></p>
</td>
<td width="378">
<p>psm array 실행 여부 확인시, package_name.procedure_name 의 형태도 인식 가능하도록 수정하였습니다.&nbsp;&nbsp;</p>
</td>
</tr>
<tr>
<td rowspan="4" width="86">
<p><strong>변경사항</strong></p>
</td>
<td width="109">
<p><strong>Performance View</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Property</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Compile Option</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Error Code</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Workaround</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<h3>BUG-46574&nbsp;Checkpoint Image 생성 도중에 서버가 비정상 종료되면 재구동에 실패 합니다.</h3>
<table width="100%">
<tbody>
<tr>
<td colspan="2" width="189">
<p><strong>Module</strong></p>
</td>
<td width="378">
<p>sm</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Category</strong></p>
</td>
<td width="378">
<p>Fatal</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>재현빈도</strong></p>
</td>
<td width="378">
<p>Always</p>
</td>
</tr>
<tr>
<td rowspan="3" width="86">
<p><strong>Reproducing Conditions</strong></p>
</td>
<td width="109">
<p><strong>재현절차</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>수행결과</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>예상결과</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>증상</strong></p>
</td>
<td width="378">
<p>Checkpoint Image 생성도중에 비정상 종료 혹은 디스크 full 등으로 헤더만 기록하고&nbsp;로그앵커 업데이트까지 진행하지 못하게 되면<br /> 디스크에는 파일이 존재하지만 로그앵커에는 없는 파일로 판단되어 재구동시 검증코드에서 비정상종료합니다. 리커버리 할때 로그앵커에 존재하지 않는 파일도 생성하도록 합니다.&nbsp;&nbsp;</p>
</td>
</tr>
<tr>
<td rowspan="4" width="86">
<p><strong>변경사항</strong></p>
</td>
<td width="109">
<p><strong>Performance View</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Property</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Compile Option</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Error Code</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Workaround</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<h3>BUG-46586&nbsp;Diag Record 관련 함수는 Function Context 의 Object 를 사용해야 합니다.</h3>
<table width="100%">
<tbody>
<tr>
<td colspan="2" width="189">
<p><strong>Module</strong></p>
</td>
<td width="378">
<p>ul-odbc</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Category</strong></p>
</td>
<td width="378">
<p>Message Error</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>재현빈도</strong></p>
</td>
<td width="378">
<p>Always</p>
</td>
</tr>
<tr>
<td rowspan="3" width="86">
<p><strong>Reproducing Conditions</strong></p>
</td>
<td width="109">
<p><strong>재현절차</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>수행결과</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>예상결과</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>증상</strong></p>
</td>
<td width="378">
<p>STF 상황에서 에러메시지가 삭제 및 추가가 서로 다른 객체 (ex. DBC, STMT)에서 일어나는 문제를 수정하였습니다.&nbsp;&nbsp;</p>
</td>
</tr>
<tr>
<td rowspan="4" width="86">
<p><strong>변경사항</strong></p>
</td>
<td width="109">
<p><strong>Performance View</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Property</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Compile Option</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Error Code</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Workaround</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<h3>BUG-46598&nbsp;V$REPGAP 퍼포먼스뷰의 REP_GAP 컬럼을 size 단위로 변경합니다.</h3>
<table width="100%">
<tbody>
<tr>
<td colspan="2" width="189">
<p><strong>Module</strong></p>
</td>
<td width="378">
<p>rp</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Category</strong></p>
</td>
<td width="378">
<p>Usability</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>재현빈도</strong></p>
</td>
<td width="378">
<p>Always</p>
</td>
</tr>
<tr>
<td rowspan="3" width="86">
<p><strong>Reproducing Conditions</strong></p>
</td>
<td width="109">
<p><strong>재현절차</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>수행결과</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>예상결과</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>증상</strong></p>
</td>
<td width="378">
<p>기존 V$REPGAP,V$REPGAP_PARALLEL의 REP_GAP은 REP_LAST_SN과 REP_SN간의 로그 일련번호의 간격입니다.&nbsp;<br /> 로그 일련번호는 내부적으로 쉬프트 연산을 포함한 비트 연산이기 때문에,&nbsp;REP_GAP이 매우 큰 값으로 나오는 문제가 있습니다.<br /> REP_GAP을 로그 일련번호의 간격에서 실제 사이즈 개념으로 수정합니다.<br /> 기본 값으로 MB 단위이며, 새로 추가된 프로퍼티 REPLICATION_GAP_UNIT을 통해 단위를 수정 할 수 있습니다.<br /> 이 값은 REP_GAP_SIZE 에서 REPLICATION_GAP_UNIT을 나눈 값으로, 나머지가 있으면 올림합니다.<br /> 또한, REP_GAP_SIZE 컬럼을 추가하여 바이트 단위의 이중화 갭도 확인할 수 있도록 수정하였습니다.&nbsp;&nbsp;</p>
</td>
</tr>
<tr>
<td rowspan="4" width="86">
<p><strong>변경사항</strong></p>
</td>
<td width="109">
<p><strong>Performance View</strong></p>
</td>
<td width="378">
<p>V$REPGAP,&nbsp;V$REPGAP_PARALLEL</p>
<p>&nbsp;</p>
<p>컬럼 수정)</p>
<p>&nbsp;</p>
<p><strong>REP_GAP</strong></p>
<p>&nbsp;</p>
<p>이중화 갭의 로그파일 사이즈를 프로퍼티 REPLICATION_GAP_UNIT에 설정된 단위로 보여준다. 기본값은 MB 단위이며 REP_GAP_SIZE에서 REPLICATION_GAP_UNIT 프로퍼티를 나눈값이다. (나머지가 있으면 올림)</p>
<p>&nbsp;</p>
<p>컬럼 추가)</p>
<p>&nbsp;</p>
<p><strong>REP_GAP_SIZE</strong>&nbsp; BIGINT</p>
<p>&nbsp;</p>
<p>이중화 갭의 로그파일 사이즈를 의미하며, BYTE 단위이다.</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Property</strong></p>
</td>
<td width="378">
<p><strong>추가</strong></p>
<p>&nbsp;</p>
<p>REPLICATION_GAP_UNIT (단위: 바이트)<br /> <br /> 데이터 타입 : Unsigned Long<br /> <br /> 기본값 : 1048576 (1MB)<br /> <br /> 속성: 변경 가능, 단일 값<br /> <br /> 값의 범위&nbsp;: [1, 2^64 -1]<br /> <br /> 설명 :&nbsp;이중화 갭의 크기를 조회하는&nbsp;REP_GAP의 값을 표현하는 단위를 설정한다.&nbsp;REP_GAP의 값은 REP_GAP_SIZE의 값을 이 프로퍼티로 나눈 결과값이며, 나머지는 올림한다.</p>
<p>&nbsp;</p>
<p>기본값이면 V$REPGAP의 REP_GAP_SIZE는 바이트 단위로, REP_GAP은 메가바이트 단위로 조회된다.</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Compile Option</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Error Code</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Workaround</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<h3>BUG-46600&nbsp;APRE PSM Array에서 User.Package.Procedure의 형태도 인식가능해야 합니다.</h3>
<table width="100%">
<tbody>
<tr>
<td colspan="2" width="189">
<p><strong>Module</strong></p>
</td>
<td width="378">
<p>mm-apre</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Category</strong></p>
</td>
<td width="378">
<p>Functionality</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>재현빈도</strong></p>
</td>
<td width="378">
<p>Always</p>
</td>
</tr>
<tr>
<td rowspan="3" width="86">
<p><strong>Reproducing Conditions</strong></p>
</td>
<td width="109">
<p><strong>재현절차</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>수행결과</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>예상결과</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>증상</strong></p>
</td>
<td width="378">
<p>apre에서 psm 호출시 user.package.psm 문법이 가능하도록 지원.&nbsp;&nbsp;</p>
</td>
</tr>
<tr>
<td rowspan="4" width="86">
<p><strong>변경사항</strong></p>
</td>
<td width="109">
<p><strong>Performance View</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Property</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Compile Option</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td width="109">
<p><strong>Error Code</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
<tr>
<td colspan="2" width="189">
<p><strong>Workaround</strong></p>
</td>
<td width="378">
<p>N/A</p>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>