# Appendix

### DB 데이터 복호화 기능

사용자로부터 DB 메시지 테이블에 데이터가 암호화되어 입력되는 경우, 복호화하는 기능에 관련하여 설정합니다.\
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

#### 1. DB\_DATA\_DECRYPTION

복호화 기능 사용 여부(방식)을 설정합니다.

* \- A(API) : 어플리케이션에서 AES 방식으로 복호화 하여 사용.
* \- P(PLUG-IN) : DBMS 에 Plug-In 방식으로 설치되어 있는 복호화 모듈(함수)를 사용.
* \- N(NONE) : 사용하지 않음.

#### 2. DB\_DATA\_DECRYPTION\_FIELDS

복호화 대상 필드 명을 설정합니다. 기본값은 MSG\_BODY 와 RE\_BODY 입니다.

복수로 입력하는 경우, |(파이프라인)로 구분하여 입력합니다. 예) MSG\_BODY|RE\_BODY

#### 3. USE\_DECRYPTION\_SEPARATION\_FIELD (Y/N)

복호화 기능을 사용하는 경우, 복호화에 대해 구분하는 필드 사용 여부를 설정합니다.\
기본 값은 Y이며, 구분하는 필드 명은 USE\_DECRYPT 입니다.

#### 4. DB\_DATA\_DECRYPTION\_FUNCTION

PLUG-IN 방식을 사용하는 경우, 복호화 모듈(함수)명을 설정합니다. 예) DECRYPT\_FUNCTION

#### 5. DB\_DATA\_DECRYPTION\_PARAMETER\_COUNT

PLUG-IN 방식을 사용하는 경우, 복호화 함수의 매개변수 개수를 설정합니다. ( 기본 : 1 )\\

#### 6. DB\_DATA\_DECRYPTION\_PARAMETER\_1

PLUG-IN 방식을 사용하는 경우, 복호화 함수의 매개변수를 입력합니다\
DB\_DATA\_DECRYPTION\_FIELDS 에 입력한 필드명 위치를 비워두시면 모듈에서 자동으로 입력합니다.

\
예 ) 함수 1 : DECRYPT\_FUNCTION(1, 'PHONE', MSG\_BODY)\
예 ) 함수 2 : DECRYPT\_FUNCTION(1, 'PHONE', RE\_BODY) DB\_DATA\_DECRYPTION\_PARAMETER\_COUNT = 3\
DB\_DATA\_DECRYPTION\_PARAMETER\_1 = 1\
DB\_DATA\_DECRYPTION\_PARAMETER\_2 = 'PHONE'\
DB\_DATA\_DECRYPTION\_PARAMETER\_3 =

#### 7. DB\_DATA\_DECRYPTION\_KEY

API 방식을 사용하는 경우, 복호화하는 키를 설정합니다.\
입력된 키는 비즈클라이언트가 정상적으로 구동되면 자동으로 암호화되어 저장됩니다.

### 백업 수행 시, 메시지 본문 길이 보관

#### 1. USE\_BACKUP\_PERSONAL\_DATA\_PROCESSING (Y/N)

발송 완료된 메시지에 대해 메시지테이블에서 로그테이블로 백업할 때,\
사용자로부터 입력된 메시지에 대해서 길이만 저장하도록 설정합니다. (대상 : MSG\_BODY, RE\_BODY)

### 첨부파일 관리 설정

#### 1. FILE\_HANDLING\_MODE

첨부파일 관리 모드를 설정합니다.

* \- 0 : DEFAULT. 첨부파일 데이터를 MSG\_TABLE 에서 관리합니다. 첨부파일 전송 시 파일명 (여러 개일 경우, '|' 문자로 구분)
* \- 1 : 첨부파일 컬럼을 추가하여 데이터를 관리합니다.\
  FILE\_PATH1 부터 FILE\_PATH5 까지의 5 개의 컬럼을 사용자가 추가해야 하며 파일명을 포함한 모든 경로를 입력해야 합니다.
* \- 2 : 첨부파일 테이블을 추가하여 첨부파일 데이터를 관리합니다.\
  첨부파일 등록 시 데이터 타입 입력이 필요하며 JSON String Type 을 사용할 수 있습니다 (여러 개의 파일 등록 시 동일한 MSG\_KEY 입력)\
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

<table><thead><tr><th width="150" align="center">MSG_KEY</th><th width="150" align="center">SEQ</th><th width="150" align="center">TYPE</th><th width="332" align="center">CONTENTS</th></tr></thead><tbody><tr><td align="center">msgKey1</td><td align="center">{숫자}</td><td align="center">FILE</td><td align="center"><strong>{첨부파일명.jpg}</strong></td></tr><tr><td align="center">msgKey1</td><td align="center">{숫자}</td><td align="center">HTTP</td><td align="center"><a href="http://www.daou.co.kr/file/jpg.jpg">http://www.daou.co.kr/file/jpg.jpg</a></td></tr><tr><td align="center">msgKey1</td><td align="center">{숫자}</td><td align="center">JSON</td><td align="center">아래 <strong>msgKey JSON</strong> 참고</td></tr></tbody></table>

**msgKey JSON**

{% hint style="info" %}
json 을 그대로 삽입할 수 있는 옵션입니다. (FILE\_HANDLING\_MODE = 2)
{% endhint %}

```json5
{
  "button": [
    {
      "name": "미리 주문하기",
      "type": "WL",
      "url_mobile": "http://www.kakao.com"
    },
    {
      "name": "상담원 연결하기",
      "type": "MD"
    },
    {
      "name": "방송 알림 설정 보기",
      "type": "AL",
      "scheme_android": "daumapps://open",
      "scheme_ios": "daumapps://open"
    }
  ]
}
```

**2. ABSOLUTE\_PATH\_OPTION (Y/N)**

첨부파일명 등록 시 상대경로/절대경로를 설정합니다.

* \- N (상대경로) : 테이블에 파일명을 입력하고 기본 경로( ./spool ) 폴더에 파일을 등록하여 사용합니다.
* \- Y (절대경로) : 테이블에 파일명을 포함한 모든 경로(ex. D:/img.jpg )를 입력하여 사용합니다.

### 모듈 재구동시 오래된 데이터 처리 옵션

#### 1. SEND\_VALID\_TIME (0 \~ 1440, MINUTE)

모듈 재구동 및 DB 세션 재 연결시 실패 처리 할 발송 유효시간을 설정합니다. (대상 컬럼 : SEND\_TIME)

* DEFAULT : 180 ( 3시간 )
* 0 : 사용하지 않음
* 1\~1440 : 재구동 시점 기준 1\~1440 분 지난 미발송 메시지 실패 처리 (결과 코드 :9034)

### 잔존 메시지 처리 옵션

네트워크 장애 및 모듈 비정상 종료 등의 사유로 백업되지 않고 메시지 테이블에 남아있는 메시지를

서버에 결과 리포트를 요청하거나 실패로 결과 처리하여 백업 테이블로 이동 되도록 하 옵션입니다. 해당 기능은 BATCH 스레드에서 5 분 간격으로 동작합니다.

{% hint style="danger" %}
해당옵션 사용시 실제 비즈서버의 통계와 고객사 DB 의 통계의 불일치가 발생할 수 있습니다.
{% endhint %}

#### 1. REPORT\_RECONFIRM\_OPTION (Y/N)

상태값(STATUS)이 1(발송 후 대기) 이고 발송시간이 55 시간(최대 리포트 타임아웃시간)이 지난 메시지에\
대해 리포트를 1회 재 요청 하고 상태값을 3으로 변경합니다.\
또한 발송시간 기준으로 3 일(클라이언트 타임아웃시간) 이내 리포트 수신이 되지 않으면 실패 결과처리를 하여 백업 테이블로 이동되도록 합니다.

* DEFAULT : N
* 결과코드 : 9023

#### 2. REPORT\_RECONFIRM\_COUNT

REPORT\_RECONFIRM\_OPTION 을 사용하는 경우 대상 메시지 FETCH COUNT

* DEFAULT : 100

#### 3. REMOVE\_PRESEND\_MSG\_OPTION (Y/N)

상태값(STATUS)이 7(발송 중)이고 발송시간이 3 일(클라이언트 타임아웃시간)이 지난 메시지에 대해 실패

결과처리를 하여 백업 테이블로 이동되도록 합니다.

* DEFAULT : N
* 결과코드 : 9037

#### 4. REMOVE\_PRESEND\_MSG\_COUNT

REMOVE\_PRESEND\_MSG\_OPTION 을 사용하는 경우 대상 메시지 FETCH COUNT

* DEFAULT : 100

#### 5. WAIT\_REPORT\_HOUR

최대 리포트 타임아웃시간(서버로부터 리포트가 수신될 수 있는 시간)을 설정합니다.

* \- DEFAULT : 55
* \- MIN : 55

#### 6. CLIENT\_TIMEOUT\_HOUR

클라이언트 타임아웃시간을 설정합니다.

* \- DEFAULT : 72
* \- MIN : 56 (WAIT\_REPORT\_HOUR + 1)

### RCS AGENCY\_ID(대행사 ID) 설정

(biz\_\_client\_\_v3000 이상)

AGENCY\_ID 는 대행사 ID 로 발신번호(chatbotId)에 대한 발송 권한이 대행사에 있는지 체크하며,\
권한 없을 시 발송 실패됩니다.\
다우기술의 대행사 ID 는 "daoutech"이며, 파라미터를 설정하지 않는 경우 해당 값으로 기본 설정됩니다.

환경 설정 파일을 수정합니다.\
**{모듈경로}/config/data/columns-{DBMS}.json**

1. RCS BUTTONS 컬럼 정보 아래 RCS AGENCY\_ID 컬럼 정보를 추가합니다.

|                                                                                                                                          기존                                                                                                                                         |                                                                                                                                             추가                                                                                                                                             |
| :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| <pre class="language-sql"><code class="lang-sql">  "constraints":"",
  "usage":"ALL"
  },{
    "description":"RCS_TABLE_RCS_BUTTON",
    "name":"BUTTONS",
    "datatype":"VARCHAR(2000)",
    "constraints":"",
    "usage":"ALL",
    "telegramKey":"BUTTONS"
  }
]
</code></pre> | <pre class="language-sql"><code class="lang-sql">  "usage":"ALL"
  "telegramKey":"BUTTONS"
  },{
    "description":"RCS_TABLE_AGENCY_ID",
    "name":"AGENCY_ID",
    "datatype":"VARCHAR(20)",
    "constraints":"",
    "usage":"ALL",
    "telegramKey":"AGENCY_ID"
  }
]
</code></pre> |

2\. 기존 BIZ\_RCS 테이블이 존재한다면\_ AGENCY\_ID VARCHAR(20) 컬럼을 추가합니다.

3\. 모듈 재 구동 후 AGENCY\_ID 컬럼에 대행사 ID를 입력하여 발송합니다.



### RESELLERCODE

**최초 발신사업자 식별코드 설정 (biz\_client\_v3015 이상)**

RESELLERCODE 는 특부가사업자 등록번호(9 자리 숫자로 구성)를 의미합니다.

1.  USE\_RESELLERCODE (Y/N) 옵션 설정 메시지 발송시 식별코드를 포함하여 전송합니다.

    \- DEFAULT : N
2.  메시지/로그 테이블 RESELLERCODE VARCHAR(10) 컬럼 추가

    \- 신규 설치시 위 옵션을 설정 후 구동하면 자동으로 추가됩니다.\
    \- 기존 테이블(BIZ\_MSG/BIZ\_LOG)이 존재한다면 테이블 삭제 후 모듈을 재구동하거나 해당 컬럼을 추가하여 발송 가능합니다.



### 중복 발송 제한 설정 (biz\_client\_v3016 이상만 해당)

중복 발송 제한 설정이란 수신번호 및 본문 내용이 동일한 메시지에 대해 첫 발송 후 일정 시간동안 발송을 차단하는 기능을 의미합니다.

* 제한 대상 메시지 타입 : SMS, LMS, MMS, AT, FT, RCS
* 버튼 및 첨부파일, 대체발송 메시지 내용은 비교하지 않습니다.

1. DUPLICATE\_SENDING\_POLICY

* 0 : DEFAULT. 중복 발송 제한 기능 사용 안함
* 1 : 수신번호 기준으로 중복 발송 제한
* 2 : 수신번호 및 메시지 내용을 기준으로 중복 발송 제한

2\. DUPLICATE\_SENDING\_MONIT\_SECONDS (30 \~ 60, SECONDS)

메시지 발송 후 동일한 메시지에 대해 모니터링하는 시간을 설정합니다.

* DEFAULT : 30
* MIN : 30
* MAX : 60

3\. DUPLICATE\_SENDING\_ALLOW\_COUNT

모니터링 시간 동안 첫 발송을 포함한 발송 허용 수를 설정합니다.

* DEFAULT : 1
* MIN : 1
