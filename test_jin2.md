<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [BUG-46120 Active Server의 hash partition 이 order 는 같고 partition 의 개수가 다를 경우 성공 합니다.](#bug-46120%C2%A0active-server%EC%9D%98-hash-partition-%EC%9D%B4-order-%EB%8A%94-%EA%B0%99%EA%B3%A0-partition-%EC%9D%98-%EA%B0%9C%EC%88%98%EA%B0%80-%EB%8B%A4%EB%A5%BC-%EA%B2%BD%EC%9A%B0-%EC%84%B1%EA%B3%B5-%ED%95%A9%EB%8B%88%EB%8B%A4)
- [BUG-46174 저장 프로시저내 insert, update 구문에서 레코드 타입변수 사용하도록 기능 확장](#bug-46174%C2%A0%EC%A0%80%EC%9E%A5-%ED%94%84%EB%A1%9C%EC%8B%9C%EC%A0%80%EB%82%B4-insert-update-%EA%B5%AC%EB%AC%B8%EC%97%90%EC%84%9C-%EB%A0%88%EC%BD%94%EB%93%9C-%ED%83%80%EC%9E%85%EB%B3%80%EC%88%98-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8F%84%EB%A1%9D-%EA%B8%B0%EB%8A%A5-%ED%99%95%EC%9E%A5)
- [BUG-46396 aexport가 생성하는 DDL 마지막 라인에 덧붙이는 newline으로 인해 iSQL에서 Syntax Error가 발생할 수 있습니다.](#bug-46396%C2%A0aexport%EA%B0%80-%EC%83%9D%EC%84%B1%ED%95%98%EB%8A%94-ddl-%EB%A7%88%EC%A7%80%EB%A7%89-%EB%9D%BC%EC%9D%B8%EC%97%90-%EB%8D%A7%EB%B6%99%EC%9D%B4%EB%8A%94-newline%EC%9C%BC%EB%A1%9C-%EC%9D%B8%ED%95%B4-isql%EC%97%90%EC%84%9C-syntax-error%EA%B0%80-%EB%B0%9C%EC%83%9D%ED%95%A0-%EC%88%98-%EC%9E%88%EC%8A%B5%EB%8B%88%EB%8B%A4)
- [BUG-46515 dumptrc을 사용해서 콜스택 출력시 altibase_error.log의 콜스택이 생략되는 경우가 있어, 이를 수정하였습니다.](#bug-46515%C2%A0dumptrc%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%95%B4%EC%84%9C-%EC%BD%9C%EC%8A%A4%ED%83%9D-%EC%B6%9C%EB%A0%A5%EC%8B%9C-altibase_errorlog%EC%9D%98-%EC%BD%9C%EC%8A%A4%ED%83%9D%EC%9D%B4-%EC%83%9D%EB%9E%B5%EB%90%98%EB%8A%94-%EA%B2%BD%EC%9A%B0%EA%B0%80-%EC%9E%88%EC%96%B4-%EC%9D%B4%EB%A5%BC-%EC%88%98%EC%A0%95%ED%95%98%EC%98%80%EC%8A%B5%EB%8B%88%EB%8B%A4)
- [BUG-46539 merge 구문에 parser conflicts 발생](#bug-46539%C2%A0merge-%EA%B5%AC%EB%AC%B8%EC%97%90-parser-conflicts-%EB%B0%9C%EC%83%9D)
- [BUG-46550 JDBC 드라이버에서 addBatch시에 directByteBuffer 사용시 메모리 증가하는 문제가 있습니다.](#bug-46550%C2%A0jdbc-%EB%93%9C%EB%9D%BC%EC%9D%B4%EB%B2%84%EC%97%90%EC%84%9C-addbatch%EC%8B%9C%EC%97%90-directbytebuffer-%EC%82%AC%EC%9A%A9%EC%8B%9C-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EC%A6%9D%EA%B0%80%ED%95%98%EB%8A%94-%EB%AC%B8%EC%A0%9C%EA%B0%80-%EC%9E%88%EC%8A%B5%EB%8B%88%EB%8B%A4)
- [BUG-46551  jdbcAdapter로 altibase 5.5.1 에 데이터 전송시 ArrayIndexOutOfBoundsException 이 발생하는 경우가 있습니다.](#bug-46551%C2%A0-jdbcadapter%EB%A1%9C-altibase-551-%EC%97%90-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%A0%84%EC%86%A1%EC%8B%9C-arrayindexoutofboundsexception-%EC%9D%B4-%EB%B0%9C%EC%83%9D%ED%95%98%EB%8A%94-%EA%B2%BD%EC%9A%B0%EA%B0%80-%EC%9E%88%EC%8A%B5%EB%8B%88%EB%8B%A4)
- [BUG-46552 isql에서 /dev/null을 사용하지 않아야 합니다](#bug-46552%C2%A0isql%EC%97%90%EC%84%9C-devnull%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%95%98%EC%A7%80-%EC%95%8A%EC%95%84%EC%95%BC-%ED%95%A9%EB%8B%88%EB%8B%A4)
- [BUG-46567 dumpStack의 mCallStackCriticalSection에 동시성문제 있음.](#bug-46567%C2%A0dumpstack%EC%9D%98-mcallstackcriticalsection%EC%97%90-%EB%8F%99%EC%8B%9C%EC%84%B1%EB%AC%B8%EC%A0%9C-%EC%9E%88%EC%9D%8C)
- [BUG-46572 APRE에서 packge를 사용시 psm array가 제대로 인식되지 않습니다.](#bug-46572%C2%A0apre%EC%97%90%EC%84%9C-packge%EB%A5%BC-%EC%82%AC%EC%9A%A9%EC%8B%9C-psm-array%EA%B0%80-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EC%9D%B8%EC%8B%9D%EB%90%98%EC%A7%80-%EC%95%8A%EC%8A%B5%EB%8B%88%EB%8B%A4)
- [BUG-46574 Checkpoint Image 생성 도중에 서버가 비정상 종료되면 재구동에 실패 합니다.](#bug-46574%C2%A0checkpoint-image-%EC%83%9D%EC%84%B1-%EB%8F%84%EC%A4%91%EC%97%90-%EC%84%9C%EB%B2%84%EA%B0%80-%EB%B9%84%EC%A0%95%EC%83%81-%EC%A2%85%EB%A3%8C%EB%90%98%EB%A9%B4-%EC%9E%AC%EA%B5%AC%EB%8F%99%EC%97%90-%EC%8B%A4%ED%8C%A8-%ED%95%A9%EB%8B%88%EB%8B%A4)
- [BUG-46586 Diag Record 관련 함수는 Function Context 의 Object 를 사용해야 합니다.](#bug-46586%C2%A0diag-record-%EA%B4%80%EB%A0%A8-%ED%95%A8%EC%88%98%EB%8A%94-function-context-%EC%9D%98-object-%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%B4%EC%95%BC-%ED%95%A9%EB%8B%88%EB%8B%A4)
- [BUG-46598 V$REPGAP 퍼포먼스뷰의 REP_GAP 컬럼을 size 단위로 변경합니다.](#bug-46598%C2%A0vrepgap-%ED%8D%BC%ED%8F%AC%EB%A8%BC%EC%8A%A4%EB%B7%B0%EC%9D%98-rep_gap-%EC%BB%AC%EB%9F%BC%EC%9D%84-size-%EB%8B%A8%EC%9C%84%EB%A1%9C-%EB%B3%80%EA%B2%BD%ED%95%A9%EB%8B%88%EB%8B%A4)
- [BUG-46600 APRE PSM Array에서 User.Package.Procedure의 형태도 인식가능해야 합니다.](#bug-46600%C2%A0apre-psm-array%EC%97%90%EC%84%9C-userpackageprocedure%EC%9D%98-%ED%98%95%ED%83%9C%EB%8F%84-%EC%9D%B8%EC%8B%9D%EA%B0%80%EB%8A%A5%ED%95%B4%EC%95%BC-%ED%95%A9%EB%8B%88%EB%8B%A4)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

<h3><br />BUG-46120&nbsp;Active Server의 hash partition 이 order 는 같고 partition 의 개수가 다를 경우 성공 합니다.</h3>
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
<p>해시파티션 이중화시 파티션갯수가 다를 경우 에러가 발생하도록 수정한다.&nbsp;&nbsp;</p>
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