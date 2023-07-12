---
description: 비즈클라이언트를 사용하기 위한 서버 요구사항
---

# 사전 준비

### 서버 요구사항

비즈클라이언트를 사용하기 위한 서버 요구사항은 아래와 같습니다.

### 하드웨어

| 운영체제   | JDK 1.8 이상 버전이 운용 가능한 OS       |
| ------ | ------------------------------ |
| CPU 유형 | 2 GHz 이상의 듀얼코어 CPU 혹은 그 이상     |
| 메모리    | 4GB 이상의 RAM 권장                 |
| 디스크 공간 | SMS 100만건 당 약 400MB의 디스크 공간 필요 |

#### 지원 가능 DBMS

* Mysql, Oracle, MSSQL -> 지원 가능
* SYBASE, DB2, DB2 AS400, CUBRID, EDB, PostgreSQL -> 버전에 따라 지원여부 상이

{% hint style="info" %}
Microsoft SQL Server 2008 이상 사용하는 경우 **DBNAME=MSSQL2005** 로 설정이 필요
{% endhint %}

{% hint style="info" %}
DBMS 의 버전에 따라 JDBC 드라이버의 JDK 요구사항이 달라질 수 있음.

**예)** 모듈의 설정파일(uds.conf)에서 **DBNAME=MSSQL2005**으로 설정된 경우, 내부적으로 Microsoft JDBC Driver 4.1 드라이버를 사용. 해당 JDBC 드라이버는 JDK 1.7 이상 필요\
또한 사용하는 DBMS 에 맞게 JDBC 드라이버를 변경하기 위해서는 다음 경로에 위치한 드라이버명과 동일하게 하여 교체 필요

\
_경로 : **{모듈위치}/lib/jdbc/{해당 JDBC 드라이버}.jar**_\
낮은 버전의 DBMS 를 지원하기 위하여 lib/jdbc 폴더의 JDBC 드라이버는 버전이 낮게 설정 되어 있으므로 정상적인 사용을 위하여 사용하는 DBMS 버전에 맞는 JDBC 드라이버를 설치 후 위와 같이 변경 필요
{% endhint %}

### 방화벽 상태 확인

* 운영 : biz.ppurio.com 18300/18400 (Outbound)
* 테스트 : biztest.ppurio.com 18300/18400 (Outbound)

### 계정 중복 여부 확인

{% hint style="info" %}
비즈클라이언트는 하나의 모듈에 비즈뿌리오 계정 하나만 세팅하도록 권장하고 있습니다.
{% endhint %}

{% hint style="info" %}
한 계정을 여러 클라이언트 모듈에 세팅할 경우 리포트가 분산되어 정상적으로 반영되지 않을 수 있습니다.
{% endhint %}



### 이모지 발송 DBMS Charset 설정

알림톡, RCS 와 같은 메시지에 이모지를 추가하여 발송하길 희망하는 경우 DB Charset을 다음과 같이 맞추어 주시길 바랍니다.

이모지 사용 가능한 메시지 타입은 [메시지발송](../dispatch/#msg\_type) 항목을 참조해 주십시오

<table><thead><tr><th width="149.66666666666666" align="center">DBMS</th><th align="center">Version</th><th align="center">Character Set</th></tr></thead><tbody><tr><td align="center">MySQL<br>MariaDB</td><td align="center">5.5.3 이상</td><td align="center">UTF8MB4_GENERAL_CI</td></tr><tr><td align="center">Oracle</td><td align="center">9i 이상</td><td align="center">AL32UTF8</td></tr><tr><td align="center">MSSQL</td><td align="center">SQL Server 2017 이상</td><td align="center">Latin1_General_100_CI_AI_SC_UTF8</td></tr></tbody></table>

