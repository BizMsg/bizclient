# Appendix



### DB 데이터 복호화 기능

사용자로부터 DB 메시지 테이블에 데이터가 암호화되어 입력되는 경우, 복호화하는 기능에 관련하여 설정합니다. \
설정파일에 존재하는 아래 항목에 대해 입력 또는 변경하여 사용하시기를 바랍니다.

```
##############################################
# DB 데이터 복호화기능 사용여부
# (A:API P:PLUGIN N:NONE)
DB_DATA_DECRYPTION = N

# 복호화 대상 필드명
DB_DATA_DECRYPTION_FIELD = 

# 암호화 구분 필드 사용여부
DB_DATA_DECRYPTION_SEPARATION_FIELD = 

# PLUGIN 방식의 경우, 함수명
DB_DATA_DECRYPTION_FUNCTION


# PLUGIN 방식의 경우, 추가 매개변수
# 복수개일 경우 |(파이프라인)로 구분하여 입력
# 예) DB_DATA_DECRYPTION_PARAMETER = 1 | 'PHONE'
DB_DATA_DECRYPTION_PARAMETER =

# PLUGIN 방식의 경우, 복호화 대상 필드명의 매개변수 위치 (기본 : 1)
DB_DATA_DECRYPTION_FIELD_LOCATION = 

# API 방식의 경우, 암호화  
DB_DATA_DECRYPTION_KEY = 
##############################################
```

####

#### DB\_DATA\_DECRYPTION

복호화 기능 사용 여부(방식)을 설정합니다.

* \-  A(API) : 어플리케이션에서 AES 방식으로 복호화 하여 사용.
* \-  P(PLUG-IN) : DBMS 에 Plug-In 방식으로 설치되어 있는 복호화 모듈(함수)를 사용.
* \-  N(NONE) : 사용하지 않음.



#### DB\_DATA\_DECRYPTION\_FIELDS

복호화 대상 필드 명을 설정합니다. 기본값은 MSG\_BODY 와 RE\_BODY 입니다.

복수로 입력하는 경우, |(파이프라인)로 구분하여 입력합니다. 예) MSG\_BODY|RE\_BODY



#### USE\_DECRYPTION\_SEPARATION\_FIELD (Y/N)

복호화 기능을 사용하는 경우, 복호화에 대해 구분하는 필드 사용 여부를 설정합니다. \
기본 값은 Y이며, 구분하는 필드 명은 USE\_DECRYPT 입니다.



#### DB\_DATA\_DECRYPTION\_FUNCTION

PLUG-IN 방식을 사용하는 경우, 복호화 모듈(함수)명을 설정합니다. 예) DECRYPT\_FUNCTION



#### DB\_DATA\_DECRYPTION\_PARAMETER\_COUNT

PLUG-IN 방식을 사용하는 경우, 복호화 함수의 매개변수 개수를 설정합니다. ( 기본 : 1 )\


#### DB\_DATA\_DECRYPTION\_PARAMETER\_1

PLUG-IN 방식을 사용하는 경우, 복호화 함수의 매개변수를 입력합니다\
DB\_DATA\_DECRYPTION\_FIELDS 에 입력한 필드명 위치를 비워두시면 모듈에서 자동으로 입력합니다.&#x20;

\
예 ) 함수 1 : DECRYPT\_FUNCTION(1, ‘PHONE’, MSG\_BODY)\
예 ) 함수 2 : DECRYPT\_FUNCTION(1, ‘PHONE’, RE\_BODY) DB\_DATA\_DECRYPTION\_PARAMETER\_COUNT = 3 \
DB\_DATA\_DECRYPTION\_PARAMETER\_1 = 1 \
DB\_DATA\_DECRYPTION\_PARAMETER\_2 = ‘PHONE’ \
DB\_DATA\_DECRYPTION\_PARAMETER\_3 =



#### DB\_DATA\_DECRYPTION\_KEY

API 방식을 사용하는 경우, 복호화하는 키를 설정합니다. \
입력된 키는 비즈클라이언트가 정상적으로 구동되면 자동으로 암호화되어 저장됩니다.





### 백업 수행 시, 메시지 본문 길이 보

#### USE\_BACKUP\_PERSONAL\_DATA\_PROCESSING (Y/N)

발송 완료된 메시지에 대해 메시지테이블에서 로그테이블로 백업할 때, \
사용자로부터 입력된 메시지에 대해서 길이만 저장하도록 설정합니다. (대상 : MSG\_BODY, RE\_BODY)



### 첨부파일 관리 설정

#### FILE\_HANDLING\_MODE

첨부파일 관리 모드를 설정합니다.

* \-  0 : DEFAULT. 첨부파일 데이터를 MSG\_TABLE 에서 관리합니다. 첨부파일 전송 시 파일명 (여러 개일 경우, ‘|’ 문자로 구분)
* \-  1 : 첨부파일 컬럼을 추가하여 데이터를 관리합니다.\
  FILE\_PATH1 부터 FILE\_PATH5 까지의 5 개의 컬럼을 사용자가 추가해야 하며 파일명을 포함한 모든 경로를 입력해야 합니다.
* \-  2 : 첨부파일 테이블을 추가하여 첨부파일 데이터를 관리합니다.\
  첨부파일 등록 시 데이터 타입 입력이 필요하며 JSONString Type 을 사용할 수 있습니다 (여러 개의 파일 등록 시 동일한 MSG\_KEY 입력)\
  \- FILE : DEFAULT. 파일명\
  \- HTTP : http/https 로 시작하는 URL\
  \- JSON : 알림톡/친구톡 발송 시 버튼 정보 JSON 데이터

> FILE\_HANDLING\_MODE = 2 사용시 AT + ATTACHMENT 발송 예 (BIZ\_MSG TABLE)



**AT + ATTACHEMENT**

```sql
INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, 
MSG_BODY, TEMPLATE_CODE, SENDER_KEY, NATION_CODE, RE_TYPE, RE_BODY, ATTACHED_FILE)

VALUES (
6, ‘201XXXXXXXXX’, NOW(), NOW(), ‘01012341234’, ‘0212341234’,
‘홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.’, {템플릿코드}, {발신프로필키}, 
‘82’, ‘MMS’, ‘[다우기술] 응모하신 프로모션에 당첨되셨습니다.’,‘msgKey1’)
```



**BIZ\_ATTACHMENTS TABLE**

| MSG\_KEY | SEQ | TYPE | CONTENTS |     |
| :------: | :-: | :--: | -------- | :-: |
|          |     |      |          |     |
|          |     |      |          |     |
|          |     |      |          |     |



**ABSOLUTE\_PATH\_OPTION (Y/N)**

첨부파일명 등록 시 상대경로/절대경로를 설정합니다.

* \-  N (상대경로) : 테이블에 파일명을 입력하고 기본 경로( ./spool ) 폴더에 파일을 등록하여 사용합니다.
* \-  Y (절대경로) : 테이블에 파일명을 포함한 모든 경로 (ex. D:/img.jpg ) 를 입력하여 사용합니다.



### 모듈 재구동시 오래된 데이터 처리 옵션

#### SEND\_VALID\_TIME (0 \~ 1440, MINUTE)

모듈 재구동 및 DB 세션 재연결시 실패처리 할 발송 유효시간을 설정합니다. (대상컬럼 : SEND\_TIME)

* &#x20;DEFAULT : 180 ( 3시간 )
* &#x20;0:사용하지않음
* &#x20;1\~1440: 재구동 시점 기준 1\~1440 분 지난 미발송 메시지 실패처리 (결과코드 :9034)



### 잔존 메시지 처리 옵

네트워크 장애 및 모듈 비정상 종료 등의 사유로 백업되지 않고 메시지 테이블에 남아있는 메시지를

서버에 결과리포트를 요청하거나 실패로 결과 처리하여 백업테이블로 이동되도록 해주는 옵션입니다. 해당 기능은 BATCH 스레드에서 5 분 간격으로 동작합니다.

{% hint style="danger" %}
해당옵션 사용시 실제 비즈서버의 통계와 고객사 DB 의 통계의 불일치가 발생할 수 있습니다.
{% endhint %}



#### REPORT\_RECONFIRM\_OPTION (Y/N)

상태값(STATUS)이 1(발송 후 대기) 이고 발송시간이 55 시간(최대 리포트 타임아웃시간)이 지난 메시지에 \
대해 리포트를 1회 재요청 하고 상태값을 3으로 변경합니다.\
또한 발송시간 기준으로 3 일(클라이언트 타임아웃시간) 이내 리포트 수신이 되지 않으면 실패 결과처리를 하여 백업테이블로 이동되도록 합니다.

* DEFAULT : N
* 결과코드 : 9023

#### REPORT\_RECONFIRM\_COUNT

REPORT\_RECONFIRM\_OPTION 을 사용하는 경우 대상 메시지 FETCH COUNT

* DEFAULT : 100

#### REMOVE\_PRESEND\_MSG\_OPTION (Y/N)

상태값(STATUS)이 7(발송 중) 이고 발송시간이 3 일(클라이언트 타임아웃시간)이 지난 메시지에 대해 실패

결과처리를 하여 백업테이블로 이동되도록 합니다.

* &#x20;DEFAULT : N
* &#x20;결과코드 : 9037

#### REMOVE\_PRESEND\_MSG\_COUNT

REMOVE\_PRESEND\_MSG\_OPTION 을 사용하는 경우 대상 메시지 FETCH COUNT

* DEFAULT : 100

#### WAIT\_REPORT\_HOUR

최대 리포트 타임아웃시간(서버로부터 리포트가 수신될 수 있는 시간)을 설정합니다.

* \-  DEFAULT : 55
* \-  MIN : 55

#### CLIENT\_TIMEOUT\_HOUR

클라이언트 타임아웃시간을 설정합니다.

* \-  DEFAULT : 72
* \-  MIN : 56 (WAIT\_REPORT\_HOUR + 1)













