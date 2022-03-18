# 카카오 비즈 메시지





### AT 발송

알림톡은 비즈뿌리오 서버에 등록된 사용 가능한 발신프로필 키와 템플릿코드를 사용하여 발송됩니다.

> 알림톡은 변수 내용을 포함하고 한글, 영어, 숫자, 특수문자 및 공백을 모두 포함하여 최대 1000 자 까지만 발송 가능합니다.

```sql
INSERT INTO biz_msg (MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, 
DEST_PHONE, SEND_PHONE, MSG_BODY, TEMPLATE_CODE, SENDER_KEY, NATION_CODE)

VALUES (6, ‘201XXXXXXXXX’, NOW(), NOW(), ‘01012341234’, ‘0212341234’,
‘홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.’, {템플릿코드}, {발신프로필키}, ‘82’)
```



**템플릿 예시**

```yaml
### 비즈뿌리오 사이트에 등록한 템플릿 내용 ###

안녕하세요 #{고객명}님 다우기술 입니다. 
#{날짜}에 주문하신 상품이 발송 되었습니다. 
택배사명 : #{택배사}
배송일자 : #{배송일}

감사합니다.
```

```
### MSG_BODY 컬럼에 입력할 내용 ###

안녕하세요 홍길동님 다우기술 입니다. 
2020.01.01 에 주문하신 상품이 발송 되었습니다. 
택배사명 : 다우택배
배송일자 : 2020.01.02

감사합니다.
```



###



### FT 발송

친구톡은 비즈뿌리오 서버에 등록된 사용 가능한 발신 프로필 키를 사용하여 발송되며, 카카오톡 사용자이고 발신 프로필(옐로우아이디 또는 플러스 친구)과 친구일 경우 발송 가능합니다.

> 친구톡은 한글, 영어, 숫자, 특수문자 및 공백을 모두 포함하여 최대 1000 자 까지만 발송 가능합니다.

```sql
INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, 
DEST_PHONE, SEND_PHONE, MSG_BODY, TEMPLATE_CODE, SENDER_KEY, NATION_CODE)

VALUES (
6, ‘201XXXXXXXXX’, NOW(), NOW(), ‘01012341234’, ‘0212341234’,
‘홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.’, {템플릿코드}, {발신프로필키}, ‘82’
```



### BI/BW (고정형) 발송

브랜드톡(고정형)은 비즈뿌리오 서버에 등록된 사용 가능한 발신프로필 키와 템플릿코드를 사용하여 발송되며발신 프로필(옐로우아이디 또는 플러스 친구)과 친구 여부에 따라 전송되는 말풍선이 모양이 달라집니다.&#x20;

> 템플릿 등록 시 텍스트 메시지, 링크 버튼, 이미지(일반, 와이드)를 등록하여 사용 가능합니다.\
> 단, 발송하는 MSG\_TYPE 과 TEMPLATE\_CODE 의 이미지 타입이 다르다면 발송이 되지 않습니다.

```sql
INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, 
DEST_PHONE, SEND_PHONE, TEMPLATE_CODE, SENDER_KEY, NATION_CODE)

VALUES (
11, ‘201XXXXXXXXX’, NOW(), NOW(), 
‘01012341234’, ‘0212341234’, {템플릿코드}, {발신프로필키}, ‘82’)
```

```sql
INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, 
DEST_PHONE, SEND_PHONE, TEMPLATE_CODE, SENDER_KEY, NATION_CODE)

VALUES (
12, ‘201XXXXXXXXX’, NOW(), NOW(), 
‘01012341234’, ‘0212341234’, {템플릿코드}, {발신프로필키}, ‘82’)
```



### BI/BW (변수형) 발송

브랜드톡(변수형)은 템플릿 본문 및 템플릿 버튼 링크에 변수가 포함된 경우 \[전문 방식], \[변수분리 방식] 중 한 가지 방식을 선택하여 발송됩니다. 브랜드톡(변수형)을 발송하고자 할 경우 환경설정파일에서 지정한 파일경로(FILE\_PATH)에 JSON 형식 파일을 업로드 한 후, 첨부될 파일은 ATTACHED\_FILE 필드에 입력합니다.

> JSON 형식 파일 인코딩은 EUC-KR 로 생성되어 있어야 합니다.\
> JSON 파일 생성이 어려운 경우 FILE\_HANDLING\_MODE 테이블을 활용 할 수 있습니다. \
> 단, 발송하는 MSG\_TYPE 과 TEMPLATE\_CODE 의 이미지 타입이 다르다면 발송이 되지 않습니다.



```sql
/// BI발송 전문 방식

INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, 
SEND_PHONE, TEMPLATE_CODE, SENDER_KEY, NATION_CODE, MSG_BODY, ATTACHED_FILE)

VALUES (
11, ‘201XXXXXXXXX’, NOW(), NOW(), 
‘01012341234’, ‘0212341234’, {템플릿코드}, {발신프로필키}, ‘82’,
‘홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다. ‘, ‘{파일명}.json’)
```



```sql
/// BW발송 변수분리 방식

INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, 
SEND_PHONE, TEMPLATE_CODE, SENDER_KEY, NATION_CODE, ATTACHED_FILE)

VALUES (
12, ‘201XXXXXXXXX’, NOW(), NOW(), 
‘01012341234’, ‘0212341234’, {템플릿코드}, {발신프로필키}, ‘82’, ‘{파일명}.json’)
```



****[**전문 방식 테이블 상세 정보**](../supplement.md#bi-bw)****



****[**변수 분리 방식 테이블 상세 정보**](../supplement.md#bi-bw-1)****



****[**파라미터 정보**](../supplement.md#bi-bw-2)****



**첨부파일 예시**

```json5
/// button.json
/// [ 브랜드톡 이미지(BI) – 전문 방식, 템플릿 본문은 MSG_BODY 입력 ]

{
  "button": [
    {
      "name": "미리 주문하기",
      "type": "WL",
      "url_mobile": "http://www.kakao.com"
    }
  ],
  "extra": {
    "msg_type": "bi",
    "content_type": "V"
  }
}
```



```json5
/// buttons.json
/// [ 브랜드톡 와이드이미지(BW) – 변수분리 방식 ]

{
  "extra": {
    "msg_type": "bw",
    "content_type": "V",
    "message_variable": {
      "name": "홍길동",
      "call": "0800000000"
    },
    "button_variable": {
      "eventmo": "https://bizmessage.kakao.com",
      "ordermo": "https://daum.net"
    }
  }
}
```





### 대체 발송 타입 (RE\_TYPE)

1차 대체발송 타입에 따라 최대 2 차 대체발송까지 가능합니다.

| 1차 대체 발송 | 2차 대체 발송 | RE\_TYPE 입력값 |
| :------: | :------: | :----------: |
|    SMS   |          |      SMS     |
|    MMS   |          |      MMS     |
|    RCS   |          |       R      |
|    RCS   |    SMS   |      RS      |
|    RCS   |    MMS   |      RM      |

### AT/FT + 1차 대체 발송

알림톡/친구톡 발송 결과 실패 시 지정하신 대체 발송 타입(SMS/MMS/RCS)과 대체 발송 본문을 사용하여 발송됩니다.

(단, 비즈뿌리오 ID 가 대체 발송 사용 가능하도록 설정되어 있어야 합니다.)

SMS/MMS 대체 발송의 경우 대체 발송 본문에 대해 동일 본문을 사용하려면, 대체 발송 메시지 필드(RE\_BODY)를 비워두시면 됩니다.

(단, SMS 대체 발송의 경우에는 메시지 본문 (MSG\_BODY) 길이가 SMS 의 허용 길이를 초과하였을 때 발송되지 않습니다.)





**AT/FT + SMS 1차 대체 발송**

```sql
AT/FT + SMS 1차 대체 발송

INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, 
SEND_PHONE, MSG_BODY, TEMPLATE_CODE, SENDER_KEY, NATION_CODE, RE_TYPE, RE_BODY)

VALUES (
6, ‘201XXXXXXXXX’, NOW(), NOW(), ‘01012341234’, ‘0212341234’,
‘홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.’, {템플릿코드}, {발신프로필키}, 
82, ‘SMS’, ‘[다우기술] 응모하신 프로모션에 당첨되셨습니다.’)
```

****

**AT/FT + MMS 1차 대체 발송**

```sql
AT/FT + MMS 1차 대체 발송

INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE,
MSG_BODY, TEMPLATE_CODE, SENDER_KEY, NATION_CODE, RE_TYPE, RE_BODY, ATTACHED_FILE)

VALUES (
6, ‘201XXXXXXXXX’, NOW(), NOW(), ‘01012341234’, ‘0212341234’,
‘홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.’, {템플릿코드}, {발신프로필키}, 
82, ‘MMS’, ‘[다우기술] 응모하신 프로모션에 당첨되셨습니다.’, {첨부파일명.jpg})
```



RCS 대체발송은 RCS 테이블의 데이터를 사용하여 메시지가 발송됩니다.

**AT/FT + RCS 1차 대체 발송**

```sql
AT/FT + RCS 1차 대체 발송

 INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, 
MSG_BODY, TEMPLATE_CODE, SENDER_KEY, NATION_CODE, RE_TYPE, RCS_REFKEY)

VALUES (
6, ‘201XXXXXXXXX’, NOW(), NOW(), ‘01012341234’, ‘0212341234’,
‘홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.’, {템플릿코드}, {발신프로필키}, 
82, ‘R’, ‘{RCS_REFKEY}’) 
```



> 대체 발송이 이루어진 경우, 클라이언트는 수신 받은 리포트를 업데이트하는 시점에 대체 발송에 대한 정보를 추가 레코드로 신규 생성하게 됩니다. \
> 알림톡/친구톡과 대체 발송에 대한 레코드의 매핑 키는 알림톡/친구톡의 UMID 필드가 대체 발송의 CMID 필드로 이루어집니다.



### AT/FT + 2차 대체 발송

알림톡/친구톡 발송 실패 시 RCS메시지를 발송하며 RCS메시지 발송 결과 실패 시 지정하신 2차 대체 발송 타입(SMS/MMS)과 대체 발송 본문을 사용하여 발송됩니다.

(단, 비즈뿌리오 ID 가 대체 발송 사용 가능하도록 설정되어 있어야 합니다.)

대체 발송 본문에 대해 동일 본문을 사용하려면, 대체 발송 메시지 필드(RE\_BODY)를 비워두시면 됩니다.

(단, SMS 대체발송의 경우에는 메시지 본문 (MSG\_BODY) 길이가 SMS 의 허용 길이를 초과하였을 때 발송되지 않습니다.)



**AT/FT + RCS(1차) + SMS(2차)**

```sql
AT/FT + RCS(1차) + SMS(2차)

INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, 
MSG_BODY, TEMPLATE_CODE, SENDER_KEY, NATION_CODE,RE_TYPE, RE_BODY, RCS_REFKEY)

VALUES (
6, ‘201XXXXXXXXX’, NOW(), NOW(), ‘01012341234’, ‘0212341234’,
‘홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.’, {템플릿코드}, {발신프로필키}, 
82, ‘RS’, ‘[다우기술] 응모하신 프로모션에 당첨되셨습니다.’, ‘{RCS_REFKEY}’)

```

> 대체 발송이 이루어진 경우, 클라이언트는 수신 받은 리포트를 업데이트하는 시점에 대체 발송에 대한 정보를 추가 레코드로 신규 생성하게 됩니다. 알림톡/친구톡과 대체 발송에 대한 레코드의 매핑 키는 알림톡/친구톡의 UMID 필드가 대체 발송의 CMID 필드로 이루어집니다.

> 2 차 대체 발송이 이루어진 경우, 알림톡/친구톡의 UMID 값 앞에 “RE\_”이 추가된 문자열이 2 차 대체 발송의 CMID 필드로 이루어지며 1 차 대체 발송의 UMID 도 같은 값으로 설정됩니다.



### BI/BW + 1차 대체 발송

브랜드톡(이미지, 와이드 이미지) 발송 결과 실패 시 지정하신 대체 발송 타입(SMS/MMS/RCS)과 대체 발송 본문을 사용하여 발송됩니다.

(단, 비즈뿌리오 ID 가 대체 발송 사용 가능하도록 설정되어 있어야 합니다.)

(단, SMS 대체발송의 경우에는 메시지 (RE\_BODY) 길이가 SMS 의 허용 길이를 초과하였을 때 발송되지 않습니다.)



**BI/BW + SMS**

```sql
INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, 
TEMPLATE_CODE, SENDER_KEY, NATION_CODE, RE_TYPE, RE_BODY)

VALUES (
11, ‘201XXXXXXXXX’, NOW(), NOW(), ‘01012341234’, ‘0212341234’,
{템플릿코드}, {발신프로필키}, ‘82’, ‘SMS’, ‘[다우기술] 응모하신 프로모션에 당첨되셨습니다.’)
```

**BI + MMS**

```sql
INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, 
TEMPLATE_CODE, SENDER_KEY, NATION_CODE,RE_TYPE, RE_BODY, ATTACHED_FILE)

VALUES (
11, ‘201XXXXXXXXX’, NOW(), NOW(), ‘01012341234’, ‘0212341234’,
{템플릿코드}, {발신프로필키}, ‘82’, ‘MMS’, 
‘[다우기술] 응모하신 프로모션에 당첨되셨습니다.’, {첨부파일명.jpg})
```



RCS 대체 발송의 경우 RCS 테이블의 데이터를 사용하여 메시지가 발송됩니다.

**BI + RCS**

```sql
INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, 
TEMPLATE_CODE, SENDER_KEY, NATION_CODE, RE_TYPE, RCS_REFKEY)

VALUES (
11, ‘201XXXXXXXXX’, NOW(), NOW(), ‘01012341234’, ‘0212341234’, 
{템플릿코드}, {발신프로필키}, ‘82’, ‘R’, ‘{RCS_REFKEY}’)
```

> BW(브랜드톡 와이드 이미지) 발송방법은 BI 와 동일하며 MSG\_TYPE 을 12 로 입력하여 발송 가능합니다.

> 대체 발송이 이루어진 경우, 클라이언트는 수신 받은 리포트를 업데이트하는 시점에 대체 발송에 **** 대한 정보를 추가 레코드로 신규 생성하게 됩니다. 브랜드톡과 대체 발송에 대한 레코드의 매핑 키는 브랜드톡의 UMID 필드가 대체 발송의 CMID 필드로 이루어집니다.





### AT/FT + ATTACHMENT 발송

알림톡/친구톡에 버튼 및 추가 기능을 사용하고자 할 경우 환경설정파일에서 지정한 파일경로(FILE\_PATH)에 JSON 형식 파일을 업로드 한 후, 첨부될 파일은 ATTACHED\_FILE 필드에 입력합니다.

(JSON 형식 파일 인코딩은 EUC-KR 로 생성되어 있어야 합니다.)

\
(웹링크, 앱링크에 변수가 있거나 JSON 파일 생성이 어려운 경우 FILE\_HANDLING\_MODE 테이블을 활용 할 수 있습니다.)&#x20;

(버튼 및 추가 기능이 등록된 템플릿코드만 사용가능합니다.)



**AT + ATTACHMENT**

```sql
INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, 
MSG_BODY, TEMPLATE_CODE, SENDER_KEY, NATION_CODE, ATTACHED_FILE)

VALUES (
6, ‘201XXXXXXXXX’, NOW(), NOW(), ‘01012341234’, ‘0212341234’,
‘홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.’, 
{템플릿코드}, {발신프로필키}, ‘82’, ‘{파일명}.json’)
```

**FT + ATTACHMENT**

```sql
INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, 
MSG_BODY, SENDER_KEY, NATION_CODE,ATTACHED_FILE)

VALUES (7, ‘201XXXXXXXXX’, NOW(), NOW(), ‘01012341234’, ‘0212341234’,
‘홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.’, 
{발신프로필키}, ‘82’, ‘{파일명}.json’)
```

****

**AT/FT ATTACHMENT 정보 및 보충자료**

