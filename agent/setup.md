# Agent Configuration

## BizPPurio Connect

```
#################################################
# 비즈클라이언트 설정 파일 (Configuration)
# Ver 3.0.1.4
# 구동시 JDK 1.8 이상 필요
#################################################

#################################################
# 운영    : biz.ppurio.com
# 검수    : biztest.ppurio.com (실발송 되지 않음)
# SSL     : 18300/18400
# NON-SSL : 15300/15400
#################################################
UDS_IP = biz.ppurio.com
UDS_SEND_PORT = 18300
UDS_RECV_PORT = 18400
UDS_ID =
UDS_PW =
USE_SSL = Y
#################################################
```

## DBMS Connect (JDBC Setting) &#x20;

{% tabs %}
{% tab title="JDBC URL" %}
```
#################################################
# JDBC 연결 정보 (필수)
#################################################
# 지원 가능한 DBMS
# MSSQL, MYSQL, ORACLE, SYBASE, CACHE, DB2, EDB, TIBERO, POSTGRES, CUBRID
# Microsoft SQL Server 2008 이상 사용하는 경우 MSSQL2005 로 설정
# 예) DBNAME = MYSQL
#
# 지원 가능한 DBMS 별 JDBC URL 예문은 다음과 같음
#  jdbc:microsoft:sqlserver://<host>:<port,1433>;DatabaseName=<db>
#  jdbc:sqlserver://<server>:<port>;databaseName=<db>
#  jdbc:mysql://<host>:<port,3306>/<db>?useUnicode=true&characterEncoding=euc-kr&useSSL=false&allowPublicKeyRetrieval=true
#  jdbc:oracle:thin:@<host>:<port,1521>:<db>
#  jdbc:sybase:Tds:<host>:<port,5000>/<db>?charset=eucksc
#  jdbc:Cache://<host>:<port,1972>/<db>
#  jdbc:db2://<host>:<port,50000>/<db>
#  jdbc:edb://<host>:<port,5444>/<db>
#  jdbc:tibero:thin:@<host>:<port,8629>:<db>
#  jdbc:postgresql://<host>:<port,5432>/<db>
#  jdbc:cubrid:<host>:<port,33000>:<server>:<db>::
#################################################
```
{% endtab %}

{% tab title="MSSQL" %}
```
##################################################################################################
DBNAME = MSSQL
DBURL = jdbc:microsoft:sqlserver://<host>:<port,1433>;DatabaseName=<db>

DBUSER =
DBPASS =
#################################################
```
{% endtab %}

{% tab title="MYSQL" %}
```
#################################################
DBNAME = MYSQL
DBURL = jdbc:mysql://<host>:<port,3306>/<db>?useUnicode=true&characterEncoding=euc-kr&useSSL=false&allowPublicKeyRetrieval=true

DBUSER =
DBPASS =
#################################################
```
{% endtab %}

{% tab title="Oracle" %}
```
#################################################
DBNAME = ORACLE
DBURL = jdbc:oracle:thin:@<host>:<port,1521>:<db>

DBUSER =
DBPASS =
#################################################

#################################################
# ORACLE 11G 이하를 사용하는 경우, Y로 변경
USE_ORACLE_PREPARED_STATEMENT = N
#################################################
```
{% endtab %}
{% endtabs %}

## Table Name Setting

```
#################################################
# 메시지/로그테이블 (필수)
#################################################
MSG_TABLE = BIZ_MSG
LOG_TABLE = BIZ_LOG
#################################################

#################################################
# RCS 테이블 (RCS 발송 시 필수)
#################################################
RCS_TABLE = BIZ_RCS
RCS_LOG_TABLE = BIZ_RCS_LOG
#################################################

#################################################
# 첨부파일 테이블 (선택)
#################################################
ATTACHMENTS_TABLE = BIZ_ATTACHMENTS
ATTACHMENTS_LOG_TABLE = BIZ_ATTACHMENTS_LOG
#################################################
```

## Threading Option

```
#################################################
# FETCH THREAD
# 전송 대상 1회 조회 건수
#################################################
FETCH_COUNT = 100
#################################################

#################################################
# SEND THREAD 개수
# 전송 세션 개수
#################################################
SEND_THREAD_COUNT = 1
#################################################

#################################################
# REPORT THREAD 개수 
#################################################
REPORT_THREAD_COUNT = 1
#################################################

#################################################
# 로그 출력 레벨 (INFO/DEBUG)
#################################################
MAIN_LOG_LEVEL = INFO
FETCH_LOG_LEVEL = INFO
SEND_LOG_LEVEL = INFO
RECV_LOG_LEVEL = INFO
REPORT_LOG_LEVEL = INFO
REORDER_LOG_LEVEL = INFO
BACKUP_LOG_LEVEL = INFO
BATCH_LOG_LEVEL = INFO
#################################################

#################################################
# WORKER 수행 여부 (Y/N)
#################################################
DO_FETCH_PROCESS = Y
DO_SEND_PROCESS = Y
DO_RECV_PROCESS = Y
DO_BACKUP_PROCESS = Y
DO_BATCH_PROCESS = Y
DO_REORDER_PROCESS = N
#################################################

#################################################
# WORKER 수행 주기 (Sleep Time, 단위:초)
#################################################
MAIN_SLEEP_SECONDS = 1
FETCH_SLEEP_SECONDS = 1
SEND_SLEEP_SECONDS = 1
RECV_SLEEP_SECONDS = 1
REPORT_SLEEP_SECONDS = 1
REORDER_SLEEP_SECONDS = 1
BACKUP_SLEEP_SECONDS = 10
#################################################
```

## Blocking Option

```
#################################################
# BLOCK TIME
# 메시지를 전송하지 않을 시간 설정
#
# BLOCK 옵션 (Y/N/D)
# Y 인 경우, 조건에 따라 실패처리
# D 인 경우, 전송가능시간에 전송
#################################################
BLOCK_OPTION = N
#################################################

#################################################
# BLOCK TIME 기준 옵션 (Y/N/S)
# Y 인 경우, SEND_TIME 기준
# N 인 경우, REQUEST_TIME 기준
# S 인 경우, 시스템 시간 기준
#################################################
BLOCK_OF_SEND_TIME =
#################################################

#################################################
# BLOCK 월
# 입력하지 않을 경우, BLOCK 하지 않으며
# 복수 선택시 콤마(,)로 구분
#
# BLCOK_MONTH 예제
#  *               모든 월 선택
#  1-6             1월에서 6월 선택
#  1-12/3          1월, 4월, 7월, 10월 선택
#  7               7월 선택
#  1-6,1-12/3,7    복수 월 선택
#################################################
BLOCK_MONTH =
#################################################

#################################################
# BLOCK 일
# 입력하지 않을 경우, BLOCK 하지 않으며
# 복수 선택시 콤마(,)로 구분
#
# BLOCK_DATE 예제
#  *                 모든 일 선택
#  1-15              1일에서 15일 선택
#  1-31/2            홀수일 선택
#  1-15,1-31/2,16    복수 일 선택
#################################################
BLOCK_DATE =
#################################################

#################################################
# BLOCK 요일별 시간
# 입력하지 않을 경우 BLOCK 하지 않으며
# 복수 선택시 콤마(,)로 구분
#
# BLOCK_TIME_DAY 예제
#  *                        모든 시간 선택
#  00:00-08:30              0시~8시 30분 선택
#  18:30-24:00              18시 30분~24시 선택
#  00:00-08:30,18:30-24:00  복수 시간 선택
#################################################
BLOCK_TIME_SUNDAY =
BLOCK_TIME_MONDAY =
BLOCK_TIME_TUESDAY =
BLOCK_TIME_WEDNESDAY =
BLOCK_TIME_THURSDAY =
BLOCK_TIME_FRIDAY =
BLOCK_TIME_SATURDAY =
#################################################

```

## Backup Option

```
#################################################
# BACKUP 옵션
# 결과 리포트 수신 및 메시지 백업
# 백업 실행 옵션 (Y/O)
# Y 인 경우 월별 백업 테이블로 데이터 이동
# O 인 경우 백업 테이블로 데이터 이동
#################################################
BACKUP_OPTION = Y
RCS_BACKUP_OPTION = N
ATTACHMENTS_BACKUP_OPTION = N

# 백업 1회 처리 개수
BACKUP_COUNT = 1000

# 백업 실행 시점 (단위:일)
# n 인 경우, 리포트 수신 후 n 일 후 백업(0 인 경우, 즉시 백업)
BACKUP_WAIT_DAY = 0
#################################################

#################################################
# 백업 수행시, 메시지 본문 길이만 보관여부 (Y/N)
USE_BACKUP_PERSONAL_DATA_PROCESSING = N
#################################################
```

## Others

```php
#################################################
# 발송 가능한 메시지 타입
# RCS 발송시 아래와 같이 설정
# 예) MESSAGE_SUPPORT_TYPE = ALL
#################################################
MESSAGE_SUPPORT_TYPE = SMS|MMS|FAX|PHONE|AT|FT|BI|BW
#################################################

#################################################
# CONVERT CHARACTER SET
# 캐릭터셋 컨버트 여부
# (한글 깨짐 현상이 없을 경우 사용하지 않는다.)
# CHARSET 예제
#  EUC-KR(= KSC5601, MS949), UTF8,
#  UTF16, 8859_1, LATIN1, ...
#################################################
CHARSET_CONV = N
FROM_CHARSET = EUC-KR
TO_CHARSET = EUC-KR
#################################################

#################################################
# LOG_PATH : 로그파일경로
# FILE_PATH : 첨부파일경로
# BLK_PATH : 블랙리스트경로
# REP_PATH : 리포트경로
#################################################
LOG_PATH = ./log
FILE_PATH = ./spool
BLK_PATH = ./blk
REP_PATH = ./rep
#################################################

#################################################
# 첨부파일 자동삭제 옵션 (Y/N)
#################################################
FILE_DELETE_OPTION = Y
#################################################

#################################################
# 리포트 재요청 사용여부 (Y/N)
REPORT_RECONFIRM_OPTION = N
REPORT_RECONFIRM_COUNT = 100
#################################################

#################################################
# 블랙리스트 사용여부 (Y/N)
BLACKLIST_USE = N
#################################################

#################################################
# 컬럼 추가 사용여부 (Y/N)
# '필드명 타입' 형태로 입력
# 복수개일 경우 |로 구분하여 입력
# 예) EXTRA_FIELD = A VARCHAR2(30)|B VARCHAR2(5)
ADD_FIELD_OPTION = N
EXTRA_FIELD = 
#################################################

#################################################
# DB 데이터 복호화기능 사용여부
# (A:API P:PLUGIN N:NONE)
DB_DATA_DECRYPTION = N

# 복호화 대상 필드명
DB_DATA_DECRYPTION_FIELDS = 

# 암호화 구분 필드 사용여부
USE_DECRYPTION_SEPARATION_FIELD = 

# PLUGIN 방식의 경우, 함수명
DB_DATA_DECRYPTION_FUNCTION = 

# PLUGIN 방식의 경우, 복호화 함수의 매개변수 개수
DB_DATA_DECRYPTION_PARAMETER_COUNT = 1

# PLUGIN 방식의 경우, 복호화 함수의 매개변수
# 매개변수 개수 만큼 넘버링하여 입력
# DB_DATA_DECRYPTION_FIELDS에 입력한 필드명의 위치는 빈칸으로 설정
DB_DATA_DECRYPTION_PARAMETER_1 = 

# API 방식의 경우, 암호화 키
DB_DATA_DECRYPTION_KEY =
#################################################

#################################################
# 첨부파일 관리 설정
# 0 : 메시지 테이블의 첨부파일 컬럼에서 관리 ( 기본 설정 )
# 1 : 메시지 테이블에 컬럼을 추가하여 관리 ( FILE_PATH1 ~ FILE_PATH5 )
# 2 : 첨부파일 테이블로 관리 ( MSG_KEY로 매칭 )
FILE_HANDLING_MODE = 0

# 첨부파일 등록시 전체경로 사용여부 (Y/N)
ABSOLUTE_PATH_OPTION = N
#################################################

#################################################
# 발송 유효시간 설정 (분 단위)
# 모듈 재구동 및 DB 세션 재연결시 발송 유효시간이 지난 미발송 메시지 실패처리
# SEND_TIME 기준
# 
# 0 : 사용하지 않음
# 1 ~ 1440 : 재구동 시점 기준 1~1440분 지난 미발송 메시지 실패처리
SEND_VALID_MINUTES = 180
#################################################

```

```python
DBURL = jdbc:mysql://<DB 호스트 IP>:<DB 호스트 PORT>/<DB 이>?useUnicode=true&
        characterEncoding=euc-kr&useSSL=false&allowPublicKeyRetrieval=true
```

RCS 발송을 활성화하기 위해선 아래와 같은 수정이 필요합니다.

```python
MESSAGE_SUPPORT_TYPE = SMS|MMS|FAX|PHONE|AT|FT|BI|BW
->
MESSAGE_SUPPORT_TYPE = ALL
```





> 클라이언트 실행 후에는 **uds.confx** 로 파일명이 변경됨
>
> * 비즈뿌리오 비밀번호나 DB 비밀번호를 수정해야 할 때 .**confx** **->** .**conf**로 변경한 뒤 수정
> * 암호화 된 비밀번호 삭제 후 재 작성

