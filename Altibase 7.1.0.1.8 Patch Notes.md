# Altibase 7.1.0.1.8 Patch Notes

*이 문서는 Sample patch notes입니다.*

기존의 패치노트는 신규 기능과 버그 fix 가 섞여서 보여졌으나, 아래와 같이 구별하려고 함.

## New Features

new features 에 해당하는 버그 list 와 changes 만 추출하여 new feature 가이드도 따로 제공할 예정.

BTS의 functionality, Efficiency, Usability, Reliability, Maintainability, Portability, Enhancement ?

개선된 기능은?
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
<p>N/A</p>
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
<p>PL/SQL 확장 기능입니다.<br /> insert/update 구문에서 레코드를 사용할 수 있도록 합니다.&nbsp;&nbsp;</p>
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

기존에는 commit 순으로 정렬되었으나, 모듈별로 정렬예정.

fatal, hang, assert, fuctional error,



## Changes

기존에는 버그 내용에 아래의 변경사항을 찾아서 보았으나,

요약본으로 Release note와 같이 아래처럼 보여주려함.

new features 에 해당하는 버그 list 와 changes 만 추출하여 new feature 가이드도 따로 제공할 예정.

### Version histories

| altibase version                   | database binary version        | meta version                   | cm protocol version            | replication protocol version   | sharding version               |
| ---------------------------------- | ------------------------------ | ------------------------------ | ------------------------------ | ------------------------------ | ------------------------------ |
| 7.1.0.1.2</br>(Released)           | 6.5.1                          | 8.5.1                          | 7.1.6                          | 7.4.2                          | 2.0.0                          |
| 7.1.0.1.3                          | 6.5.1                          | 8.5.1                          | 7.1.6                          | 7.4.2                          | 2.0.0                          |
| 7.1.0.1.4                          | 6.5.1                          | 8.6.1                          | 7.1.6                          | 7.4.3                          | 2.1.0                          |
| 7.1.0.1.5                          | 6.5.1                          | 8.6.1                          | 7.1.6                          | 7.4.3                          | 2.1.0                          |
| 7.1.0.1.6                          | 6.5.1                          | 8.6.1                          | 7.1.6                          | 7.4.3                          | 2.1.0                          |
| 7.1.0.1.7                          | 6.5.1                          | 8.6.1                          | 7.1.6                          | 7.4.3                          | 2.1.0                          |
| <font color="red">7.1.0.1.8</font> | <font color="red">6.5.1</font> | <font color="red">8.7.1</font> | <font color="red">7.1.6</font> | <font color="red">7.4.4</font> | <font color="red">2.1.0</font> |

### 호환성

변경이 있는 경우에만 기술한다.

#### 	Meta Version

메타 버전이 8.6.1 에서 8.7.1로 변경되었다. 7.1.0.1.7 이하에서 7.1.0.1.8로 패치하면, 자동으로 메타 업그레이드가 수행된다. 

> 패치를 롤백하려는 경우, [메타다운그레이드](https://github.com/ALTIBASE/Documents/blob/master/Manuals/Altibase_7.1/kor/Installation.md#%EB%A9%94%ED%83%80-%EB%8B%A4%EC%9A%B4%EA%B7%B8%EB%A0%88%EC%9D%B4%EB%93%9Cmeta-downgrade)를 참고한다.

#### 	CM protocol Version

통신프로토콜 버전이 변경되었지만, 하위 호환성을 보장한다.

#### 	Replication protocol Version

이중화 프로토콜 버전이 변경되었지만, 하위 호환성을 보장한다.

#### 	Sharding Version

샤딩 버전은 변경되지 않았다. 단, 7.1.0.1.3 이하에서 7.1.0.1.8로 패치하려는 경우, 샤딩은 재구성해야 한다.

> 알티베이스 샤딩 프로토콜 및 메타는 상위, 하위 호환성을 보장하지 않는다. 즉, 샤딩 버전이 다른 경우, 재구성해야 한다.

#### 	Client Application

매뉴얼의 Application Development 아래 내용중 API 및 driver, packages, procedure 관련 호환성 이슈 있는 것만 기록합니다. 변경이 있는 경우에만 기술한다. (주로 수동으로 작성해야 함... )

헤더 파일이 변경되는 경우

API 함수의 변경이 있는 경우

##### 	JDBC Driver

##### 	CLI

##### 	Apre

##### 	Spatial API

##### 	Packages

##### 	Stored Procedures

##### 	ACI

##### 	ODBC Driver

### 프로퍼티

요약해서, 추가된,수정된,삭제된 프로퍼티 보여준다. (추후 자동 가능)

### 성능 뷰

요약해서, 추가된,수정된,삭제된 성능뷰 보여준다. (추후 자동 가능)

### 메타테이블

변경이 있는 경우에만 기술한다.

## Known Issues

