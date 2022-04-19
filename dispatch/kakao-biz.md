---
description: 알림톡/친구톡
---

# 카카오 비즈 메시지

### AT 발송

알림톡은 비즈뿌리오 서버에 등록된 사용 가능한 **발신프로필 키**와 **템플릿코드**를 사용하여 발송됩니다.

> 알림톡은 변수 내용을 포함하고 한글, 영어, 숫자, 특수문자 및 공백을 모두 포함하여 최대 1000 자 까지만 발송 가능합니다.

```sql
INSERT INTO biz_msg (MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, 
DEST_PHONE, SEND_PHONE, MSG_BODY, TEMPLATE_CODE, SENDER_KEY, NATION_CODE)

VALUES (6, '201XXXXXXXXX', NOW(), NOW(), '01012341234', '0212341234',
'홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.', {템플릿코드}, {발신프로필키}, '82')
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



### FT 발송

친구톡은 비즈뿌리오 서버에 등록된 사용 가능한 **발신 프로필 키**를 사용하여 발송되며, 카카오톡 사용자이고 발신 프로필(옐로우아이디 또는 플러스 친구)과 **친구일 경우** 발송 가능합니다.

> 친구톡은 한글, 영어, 숫자, 특수문자 및 공백을 모두 포함하여 최대 1000 자 까지만 발송 가능합니다.

```sql
INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, 
DEST_PHONE, SEND_PHONE, MSG_BODY, TEMPLATE_CODE, SENDER_KEY, NATION_CODE)

VALUES (
6, '201XXXXXXXXX', NOW(), NOW(), '01012341234', '0212341234',
'홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.', {템플릿코드}, {발신프로필키}, '82'
```



### BI/BW (고정형) 발송

브랜드톡(고정형)은 비즈뿌리오 서버에 등록된 사용 가능한 **발신프로필 키**와 **템플릿코드**를 사용하여 발송되며 발신 프로필(옐로우아이디 또는 플러스 친구)과 **친구 여부에 따라** 전송되는 말풍선이 모양이 달라집니다.&#x20;

> 템플릿 등록 시 텍스트 메시지, 링크 버튼, 이미지(일반, 와이드)를 등록하여 사용 가능합니다.\
> 단, 발송하는 **MSG\_TYPE** 과 **TEMPLATE\_CODE** 의 이미지 타입이 다르다면 발송이 되지 않습니다.

```sql
INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, 
DEST_PHONE, SEND_PHONE, TEMPLATE_CODE, SENDER_KEY, NATION_CODE)

VALUES (
11, '201XXXXXXXXX', NOW(), NOW(), 
'01012341234', '0212341234', {템플릿코드}, {발신프로필키}, '82')
```

```sql
INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, 
DEST_PHONE, SEND_PHONE, TEMPLATE_CODE, SENDER_KEY, NATION_CODE)

VALUES (
12, '201XXXXXXXXX', NOW(), NOW(), 
'01012341234', '0212341234', {템플릿코드}, {발신프로필키}, '82')
```



### BI/BW (변수형) 발송

브랜드톡(변수형)은 템플릿 본문 및 템플릿 버튼 링크에 변수가 포함된 경우 \[**전문 방식**], \[**변수분리 방식**] 중 한 가지 방식을 선택하여 발송됩니다. 브랜드톡(변수형)을 발송하고자 할 경우 환경설정파일에서 지정한 파일경로(FILE\_PATH)에 JSON 형식 파일을 업로드 한 후, 첨부될 파일은 **ATTACHED\_FILE** 필드에 입력합니다.

> JSON 형식 파일 인코딩은 **EUC-KR** 로 생성되어 있어야 합니다.\
> JSON 파일 생성이 어려운 경우 **FILE\_HANDLING\_MODE** 테이블을 활용 할 수 있습니다. \
> 단, 발송하는 **MSG\_TYPE** 과 **TEMPLATE\_CODE** 의 이미지 타입이 다르다면 **발송이 되지 않습니다.**



```sql
/// BI발송 전문 방식

INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, 
SEND_PHONE, TEMPLATE_CODE, SENDER_KEY, NATION_CODE, MSG_BODY, ATTACHED_FILE)

VALUES (
11, '201XXXXXXXXX', NOW(), NOW(), 
'01012341234', '0212341234', {템플릿코드}, {발신프로필키}, '82',
'홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.', '{파일명}.json')
```



```sql
/// BW발송 변수분리 방식

INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, 
SEND_PHONE, TEMPLATE_CODE, SENDER_KEY, NATION_CODE, ATTACHED_FILE)

VALUES (
12, '201XXXXXXXXX', NOW(), NOW(), 
'01012341234', '0212341234', {템플릿코드}, {발신프로필키}, '82', '{파일명}.json')
```





### 전문 방식 전송정보 (BI/BW 변수형)

MSG\_BODY는 메시지 테이블의 컬럼이며 \[전문 방식]의 템플릿 본문이 입력되어야 합니다.

| 본문에 변수 존재 | 버튼에 변수 존재 |        필수 파라미터        |
| :-------: | :-------: | :-------------------: |
|     O     |     O     | MSG\_BODY(DB), button |
|     O     |     X     |     MSG\_BODY(DB)     |
|     X     |     O     |         button        |
|     X     |     X     |                       |

### 변수분리 방식 전송정보 (BI/BW 변수형)

| 본문에 변수 존재 | 버튼에 변수 존재 |                   필수 파라미터                   |
| :-------: | :-------: | :-----------------------------------------: |
|     O     |     O     | <p>message_variable,<br>button_variable</p> |
|     O     |     X     |              message\_variable              |
|     X     |     O     |               button\_variable              |
|     X     |     X     |                                             |

### 파라미터 정보 (BI/BW 변수형)

|                 키                |  타입  |  필수 |                     설명                     |
| :------------------------------: | :--: | :-: | :----------------------------------------: |
|              button              |      |  N  |      \*5.6.6 AT/FT + ATTACHMENT 발송 참조      |
|     <p>extra<br>msg_type</p>     | TEXT |  Y  | <p>메시지 발송 타입 <br>(BI: 이미지, BW: 와이드이미지)</p> |
|   <p>extra<br>content_type</p>   | TEXT |  Y  |           텍스트 유형 (F: 고정형, V: 변수형)          |
| <p>extra<br>message_variable</p> | JSON |  N  |               템플릿 본문에 포함된 변수값              |
|  <p>extra<br>button_variable</p> | JSON |  N  |             템플릿 버튼 링크에 포함된 변수값             |



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

필수 파라미터가 아닌 것이 포함된 경우 불필요한 파라미터 입력 에러로 발송이 실패할 수 있습니다.



### 대체 발송 타입 (RE\_TYPE)

1차 대체발송 타입에 따라 최대 2차 대체발송까지 가능합니다.

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
6, '201XXXXXXXXX', NOW(), NOW(), '01012341234', '0212341234',
'홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.', {템플릿코드}, {발신프로필키}, 
82, 'SMS', '[다우기술] 응모하신 프로모션에 당첨되셨습니다.')
```

****

**AT/FT + MMS 1차 대체 발송**

```sql
AT/FT + MMS 1차 대체 발송

INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE,
MSG_BODY, TEMPLATE_CODE, SENDER_KEY, NATION_CODE, RE_TYPE, RE_BODY, ATTACHED_FILE)

VALUES (
6, '201XXXXXXXXX', NOW(), NOW(), '01012341234', '0212341234',
'홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.', {템플릿코드}, {발신프로필키}, 
82, 'MMS', '[다우기술] 응모하신 프로모션에 당첨되셨습니다.', {첨부파일명.jpg})
```



RCS 대체발송은 RCS 테이블의 데이터를 사용하여 메시지가 발송됩니다.

**AT/FT + RCS 1차 대체 발송**

```sql
AT/FT + RCS 1차 대체 발송

 INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, 
MSG_BODY, TEMPLATE_CODE, SENDER_KEY, NATION_CODE, RE_TYPE, RCS_REFKEY)

VALUES (
6, '201XXXXXXXXX', NOW(), NOW(), '01012341234', '0212341234',
'홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.', {템플릿코드}, {발신프로필키}, 
82, 'R', '{RCS_REFKEY}') 
```



> 대체 발송이 이루어진 경우, 클라이언트는 수신 받은 리포트를 업데이트하는 시점에 대체 발송에 대한 정보를 추가 레코드로 신규 생성하게 됩니다. \
> 알림톡/친구톡과 대체 발송에 대한 레코드의 매핑 키는 알림톡/친구톡의 UMID 필드가 대체 발송의 CMID 필드로 이루어집니다.



### AT/FT + 2차 대체 발송

알림톡/친구톡 발송 실패 시 RCS메시지를 발송하며 RCS메시지 발송 결과 실패 시 지정한 2차 대체 발송 타입(SMS/MMS)과 대체 발송 본문을 사용하여 발송됩니다.\
(단, 비즈뿌리오 ID 가 대체 발송 사용 가능하도록 설정되어 있어야 합니다.)

대체 발송 본문에 대해 동일 본문을 사용하려면, 대체 발송 **메시지 필드**(RE\_BODY)를 비워두시면 됩니다.\
(단, SMS 대체발송의 경우에는 **메시지 본문**(MSG\_BODY) 길이가 SMS 의 허용 길이를 초과하였을 때 발송되지 않습니다.)



**AT/FT + RCS(1차) + SMS(2차)**

```sql
AT/FT + RCS(1차) + SMS(2차)

INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, 
MSG_BODY, TEMPLATE_CODE, SENDER_KEY, NATION_CODE,RE_TYPE, RE_BODY, RCS_REFKEY)

VALUES (
6, '201XXXXXXXXX', NOW(), NOW(), '01012341234', '0212341234',
'홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.', {템플릿코드}, {발신프로필키}, 
82, 'RS', '[다우기술] 응모하신 프로모션에 당첨되셨습니다.', '{RCS_REFKEY}')

```

> 대체 발송이 이루어진 경우, 클라이언트는 수신 받은 리포트를 업데이트하는 시점에 대체 발송에 대한 정보를 추가 레코드로 신규 생성하게 됩니다. 알림톡/친구톡과 대체 발송에 대한 레코드의 매핑 키는 알림톡/친구톡의 **UMID** 필드가 대체 발송의 **CMID** 필드로 이루어집니다.

> 2차 대체 발송이 이루어진 경우, 알림톡/친구톡의 **UMID** 값 앞에 "**RE\_"**이 추가된 문자열이 2차 대체 발송의 **CMID** 필드로 이루어지며 1차 대체 발송의 **UMID** 도 같은 값으로 설정됩니다.



### BI/BW + 1차 대체 발송

브랜드톡(이미지, 와이드 이미지) 발송 결과 실패 시 지정하신 **대체 발송 타입**(SMS/MMS/RCS)과 **대체 발송 본문**을 사용하여 발송됩니다.

(단, 비즈뿌리오 ID 가 대체 발송 사용 가능하도록 설정되어 있어야 합니다.)

(단, SMS 대체발송의 경우에는 메시지(RE\_BODY) 길이가 SMS 의 허용 길이를 초과하였을 때 발송되지 않습니다.)



**BI/BW + SMS**

```sql
INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, 
TEMPLATE_CODE, SENDER_KEY, NATION_CODE, RE_TYPE, RE_BODY)

VALUES (
11, '201XXXXXXXXX', NOW(), NOW(), '01012341234', '0212341234',
{템플릿코드}, {발신프로필키}, '82', 'SMS', '[다우기술] 응모하신 프로모션에 당첨되셨습니다.')
```

**BI + MMS**

```sql
INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, 
TEMPLATE_CODE, SENDER_KEY, NATION_CODE,RE_TYPE, RE_BODY, ATTACHED_FILE)

VALUES (
11, '201XXXXXXXXX', NOW(), NOW(), '01012341234', '0212341234',
{템플릿코드}, {발신프로필키}, '82', 'MMS', 
'[다우기술] 응모하신 프로모션에 당첨되셨습니다.', {첨부파일명.jpg})
```



RCS 대체 발송의 경우 RCS 테이블의 데이터를 사용하여 메시지가 발송됩니다.

**BI + RCS**

```sql
INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, 
TEMPLATE_CODE, SENDER_KEY, NATION_CODE, RE_TYPE, RCS_REFKEY)

VALUES (
11, '201XXXXXXXXX', NOW(), NOW(), '01012341234', '0212341234', 
{템플릿코드}, {발신프로필키}, '82', 'R', '{RCS_REFKEY}')
```

> BW(브랜드톡 와이드 이미지) 발송방법은 BI 와 동일하며 **MSG\_TYPE**을 **12**로 입력하여 발송 가능합니다.

> 대체 발송이 이루어진 경우, 클라이언트는 수신 받은 리포트를 업데이트하는 시점에 대체 발송에 **** 대한 정보를 추가 레코드로 신규 생성하게 됩니다. 브랜드톡과 대체 발송에 대한 레코드의 매핑 키는 브랜드톡의 **UMID** 필드가 대체 발송의 **CMID** 필드로 이루어집니다.





### AT/FT + ATTACHMENT 발송

알림톡/친구톡에 버튼 및 추가 기능을 사용하고자 할 경우 환경설정 파일에서 지정한 파일경로(FILE\_PATH)에 JSON 형식 파일을 업로드 한 후, 첨부될 파일은 **ATTACHED\_FILE** 필드에 입력합니다.

(JSON 형식 파일 인코딩은 **EUC-KR** 로 생성되어 있어야 합니다.)

\
(웹 링크, 앱 링크에 변수가 있거나 JSON 파일 생성이 어려운 경우 **FILE\_HANDLING\_MODE** 테이블을 활용 할 수 있습니다.)&#x20;

(버튼 및 추가 기능이 등록된 템플릿코드만 사용가능합니다.)



**AT + ATTACHMENT**

```sql
INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, 
MSG_BODY, TEMPLATE_CODE, SENDER_KEY, NATION_CODE, ATTACHED_FILE)

VALUES (
6, '201XXXXXXXXX', NOW(), NOW(), '01012341234', '0212341234',
'홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.', 
{템플릿코드}, {발신프로필키}, '82', '{파일명}.json')
```

**FT + ATTACHMENT**

```sql
INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, 
MSG_BODY, SENDER_KEY, NATION_CODE,ATTACHED_FILE)

VALUES (7, '201XXXXXXXXX', NOW(), NOW(), '01012341234', '0212341234',
'홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.', 
{발신프로필키}, '82', '{파일명}.json')
```

****

### AT/FT ATTACHMENT 정보

Key:supplement 항목은 아래 이어지는 supplement 테이블을 참고&#x20;



|        키        |        키        |      키      |    타입    |  필수 |                                                                설명                                                                |
| :-------------: | :-------------: | :---------: | :------: | :-: | :------------------------------------------------------------------------------------------------------------------------------: |
|      button     |                 |             |   array  |  -  |                                                               버튼 목록                                                              |
|                 |       name      |             | text(14) |  Y  |                                    <p>버튼 제목</p><p><strong>‘AC’ 타입인 경우 ‘채널 추가’로 고정</strong></p>                                   |
|                 |       type      |             |  text(2) |  Y  |                                          <p>버튼타입<br><strong>아래 타입 별 속성 표 참조</strong></p>                                         |
|                 |     url\_pc     |             |   text   |  -  |                                                      PC 환경에서 버튼 클릭 시 이동할 URL                                                     |
|                 |   url\_mobile   |             |   text   |  -  |                                                    Mobile 환경에서 버튼 클릭 시 이동할 URL                                                   |
|                 |   scheme\_ios   |             |   text   |  -  |                                       Mobile Ios 환경에서 버튼 클릭 시 실행할 Application Custom Scheme                                      |
|                 | scheme\_android |             |   text   |  -  |                                     Mobile Android 환경에서 버튼 클릭 시 실행할 Application Custom Scheme                                    |
|                 |   chat\_extra   |             | text(50) |  -  |                                                        상담톡/봇 전환 시 전달할 메타정보                                                       |
|                 |   chat\_event   |             | text(50) |  -  |                                                         봇 전환 시 연결할 봇 이벤트명                                                        |
|                 |    plugin\_id   |             | text(24) |  -  |                                                              플러그인 ID                                                             |
|                 |    relay\_id    |             |   text   |  -  |                                          플러그인 실행시 X-Kakao-Plugin-Relay-Id 헤더를 통해 전달 받을 값                                         |
|                 |   oneclick\_id  |             |   text   |  -  |                                                     원클릭 결제 플러그인에서 사용하는 결제 정보                                                     |
|                 |   product\_id   |             |   text   |  -  |                                                     원클릭 결제 플러그인에서 사용하는 결제 정보                                                     |
|      image      |                 |             |   json   |  N  |                                                              친구톡 이미지                                                             |
|                 |     Img\_url    |             |   text   |  Y  |                                    <p>노출할 이미지 <br><strong>친구톡 이미지(와이드) 발송 시 필수입력</strong></p>                                    |
|                 |    Img\_link    |             |   text   |  N  |                                        <p>이미지 클릭시 이동할 url</p><p>미설정시 카카오톡 내 이미지 뷰어 사용</p>                                        |
| item\_highlight |                 |             |   json   |  N  |                                                             아이템 하이라이트                                                            |
|                 |      title      |             | text(30) |  Y  |                                                      타이틀 (이미지가 있는 경우 최대 21자)                                                     |
|                 |   description   |             | text(19) |  Y  |                                                     부가정보 (이미지가 있는 경우 최대 14자)                                                     |
|       item      |                 |             |   json   |  N  |                                                         아이템리스트와 아이템 요약정보                                                         |
|                 |       list      |             |   array  |  Y  |                                                              아이템리스트                                                              |
|                 |                 |    title    |  text(6) |  Y  |                                                                타이틀                                                               |
|                 |                 | description | text(23) |  Y  |                                                               부가정보                                                               |
|                 |     summary     |             |   json   |  N  |                                                             아이템 요약정보                                                             |
|                 |                 |    title    |  text(6) |  Y  |                                                                타이틀                                                               |
|                 |                 | description | text(14) |  Y  | <p></p><p>가격정보</p><p><em>허용되는 문자: 통화기호(유니코드 통화기호, 元, 円, 원), 통화코드(ISO 4217), 숫자, 콤마, 소수점, 공백</em></p><p><em>소수점 2자리까지 허용</em></p> |
|      extra      |                 |             |   json   |  -  |                                                               추가 기능                                                              |
|                 |    msg\_type    |             |   text   |     |                                 <p></p><p>카카오 발송 유형</p><p><strong>알림톡 이미지 발송 시 필수입력</strong></p>                                 |
|                 |      title      |             | text(50) |     |                                                       템플릿 내용 중 강조 표기할 핵심 정보                                                      |
|                 |    supplement   |             |   json   |     |                                     <p>메시지에 첨부할 바로연결</p><p><strong>supplement 참조</strong></p>                                    |
|                 |      price      |             |  number  |     |                                         <p>모먼트 광고 전환 최적화 전용 <br>메시지 내 포함된 가격/금액/결제금액</p>                                         |
|                 |  currency\_type |             |  text(3) |     |                        <p>모먼트 광고 전환 최적화 전용 <br>메시지 내 포함된 가격/금액/결제금액의 통화단위 KRW, USD, EUR 등 국제 통화 코드 사용</p>                        |
|                 |      header     |             | text(16) |     |                                                          메시지 상단에 표기할 제목                                                          |

**supplement**

|       키      |        키        |    타입    |  필수 |                                 설명                                |
| :----------: | :-------------: | :------: | :-: | :---------------------------------------------------------------: |
| quick\_reply |       name      | text(14) |  Y  |                              바로연결 제목                              |
|      ''      |       type      |  text(2) |  Y  |                              바로연결 타입                              |
|      ''      | scheme\_android |   text   |     |    mobile android 환경에서 바로연결 클릭 시 실행할 application custom scheme    |
|      ''      |   scheme\_ios   |   text   |     | <p>mobile ios 환경에서 바로연결 클릭 시 실행할<br>application custom scheme</p> |
|      ''      |   url\_mobile   |   text   |     |                   mobile 환경에서 바로연결 클릭 시 이동할 url                   |
|      ''      |     url\_pc     |   text   |     |                      pc 환경에서 버튼 클릭 시 이동할 url                      |
|      ''      |   chat\_extra   | text(50) |     |                        상담톡/봇 전환 시 전달할 메타정보                        |
|      ''      |   chat\_event   | text(50) |     |                         봇 전환 시 연결할 봇 이벤트명                         |

### **AT/FT + BUTTON**

**버튼 타입**

|   타입   |                                                                   기능                                                                   |
| :----: | :------------------------------------------------------------------------------------------------------------------------------------: |
|  배송조회  |                           <ul><li>메시지 내용에 택배사명과 송장 번호를 파싱하여 카카오 검색 배송조회 페이지로 <br>이동하는 버튼을 자동으로 생성함</li></ul>                           |
|  웹 링크  |   <ul><li>버튼 클릭 시 인앱 브라우저에서 웹 페이지 실행</li><li><p>Mobile / PC에서 실행할 URL을 각각 설정 가능</p><p>*현재 알림톡은 PC 에서 메시지 내용이 보이지 않음<br></p></li></ul>  |
|  앱 링크  |                 <p></p><ul><li>버튼 클릭 시 앱 Custom Scheme 실행</li><li>Android /Ios 에서 실행할 Custom Scheme 각각 설정 필수</li></ul>                 |
|  봇 키워드 |          <ul><li>버튼 클릭 시 유저로부터 '<strong>버튼 명</strong>'이 텍스트로 들어간 챗버블이 발송됨</li><li>봇 또는 상담원에게 유저의 액션을 전달할 때 사용할 수 있음</li></ul>          |
| 메시지 전달 | <ul><li>버튼 클릭 시 유저로부터 '<strong>버튼 명+메시지 본문</strong>'이 텍스트로 들어간 챗버블이 발송됨</li><li>봇 또는 상담원에게 유저가 수신한 알림톡과 함께 유저의 액션을 전달할 경우 사용</li></ul> |
|  채널 추가 |                                                   <ul><li>카카오톡 채널 추가 버튼 활성화</li></ul>                                                  |
| 상담톡 전환 |                                   <ul><li>버튼 클릭 시 상담톡으로 전환</li><li>상담톡을 이용하는 카카오톡 채널만 이용 가능</li></ul>                                  |
|  봇 전환  |                         <ul><li>상담톡을 이용하는 카카오톡 채널만 이용 가능</li><li>카카오 I 오픈빌더의 챗봇을 사용하는 카카오톡 채널만 이용 가능</li></ul>                         |
|   플러그  |                          <ul><li>버튼 클릭 시 플러그인 제공</li><li>이미지 보안 전송 플러그인, 개인 정보 이용 플러그인, 원클릭 결제 플러그인</li></ul>                          |



### AT/FT + 버튼 타입별 속성

|  타입 |        속성       |  타입  |  필수 |                                 설명                                 |
| :-: | :-------------: | :--: | :-: | :----------------------------------------------------------------: |
|  WL |   url\_mobile   | text |  Y  |                  버튼 클릭 시 이동할 pc/mobile환경별 Web URL                  |
|  WL |     url\_pc     | text |  N  |                  버튼 클릭 시 이동할 pc/mobile환경별 Web URL                  |
|  AL |   scheme\_ios   | text |  Y  |             버튼 클릭 시 실행할 OS 별 Application Custom Scheme             |
|  AL | scheme\_android | text |  Y  |             버튼 클릭 시 실행할 OS 별 Application Custom Scheme             |
|  DS |        -        |   -  |  -  |                        버튼 클릭 시 배송조회 페이지로 이동                        |
|  BK |        -        |   -  |  -  |                            해당 버튼 텍스트 전송                            |
|  MD |        -        |   -  |  -  |                         해당 버튼 텍스트+메시지본문 전송                         |
|  AC |        -        |   -  |  -  |                         버튼 클릭 시 카카오톡 채널 추가                         |
|  BC |   chat\_extra   | text |  N  |                          상담톡 전환 시 전달할 메타정보                         |
|  BT |   chat\_extra   | text |  N  |                           봇 전환 시 전달할 메타정보                          |
|  BT |   chat\_event   | text |  N  |                          봇 전환 시 연결할 봇 이벤트명                         |
|  P1 |        -        |   -  |  -  |                           이미지 보안 전송 플러그인                           |
|  P2 |        -        |   -  |  -  |                             개인정보이용 플러그인                            |
|  P3 |        -        |   -  |  -  | <p>원클릭 결제 플러그인<br>(발송시 oneclick_id 또는 product_id 를 필수로 전달해아 함)</p> |

#### 버튼 첨부파일 예시

**button.json**

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

****

****

### **AT + 바로연결**

****

알림톡 바로연결이란?

* 알림톡 하단에 가로 슬라이드 형태로 표시되며 웹/앱 연결, 상담톡 전환 등을 호출하는 기능&#x20;
* 상담톡 또는 챗봇을 사용하는 발신프로필만 이용 가능
* 바로연결은 최대 10개까지 사용 가능, 사용 시 버튼 개수는 2개로 제한 \
  ****(챗봇, 상담톡 사용 채널에만 한해 사용 가능합니다.)

### AT + 바로연결 타입별 속성

|  타입 |        속성       |  타입  |  필수 |                      설명                      |
| :-: | :-------------: | :--: | :-: | :------------------------------------------: |
|  WL |   url\_mobile   | text |  Y  |      바로연결 클릭 시 이동할 pc/mobile 환경별 web url     |
|  WL |     url\_pc     | text |  N  |      바로연결 클릭 시 이동할 pc/mobile 환경별 web url     |
|  AL |   scheme\_ios   | text |  -  | 바로연결 클릭 시 실행할 OS 별 Application Custom Scheme |
|  AL | scheme\_android | text |  -  | 바로연결 클릭 시 실행할 OS 별 Application Custom Scheme |
|  AL |   url\_mobile   | text |  -  |         mobile 환경에서 바로연결 클릭 시 이동할 url        |
|  AL |     url\_pc     | text |  N  |           pc 환경에서 바로연결 클릭 시 이동할 url          |
|  BK |        -        |   -  |  -  |                해당 바로연결 텍스트 전송                |
|  MD |        -        |   -  |  -  |             해당 바로연결 텍스트+메시지 본문 전송            |
|  BC |   chat\_extra   | text |  N  |               상담톡 전환 시 전달할 메타정보              |
|  BT |   chat\_extra   | text |  N  |                봇 전환 시 전달할 메타정보               |
|  BT |   chat\_event   | text |  N  |               봇 전환 시 연결할 봇 이벤트명              |

**바로연결 첨부파일 예시**

**quick\_reply.json**

```json5
{
  "button": [
    {
      "name": "비즈뿌리오 바로가기",
      "type": "WL",
      "url_mobile": "https://www.bizppurio.com/"
    }
  ],
  "extra": {
    "supplement": {
      "quick_reply": [
        {
          "name": "비즈뿌리오",
          "type": "WL",
          "url_mobile": "https://www.bizppurio.com/"
        },
        {
          "type": "BK"
        },
        {
          "name": "메시지전달하기",
          "type": "MD"
        },
        {
          "name": "상담톡전환",
          "type": "BC"
        }
      ]
    }
  }
}

```

****

### AT + 강조 표기

템플릿 내용 중 강조 표기할 핵심 정보\
(메시지 강조 표기 타이틀은 최대 50 자 까지 설정 가능하며 알림톡 본문(1000 자)에 포함되지 않습니다.)

**강조 표기 첨부파일 예시**

**Title.json (버튼이 없는 경우)**

```json5
{
  "extra" : {
    "title" : "입금 123,456 원"
  }
}
```



**Title.json (버튼이 있는 경우)**

```json5
{
  "button": [
    {
      "name": "채널 추가",
      "type": "AC"
    }
  ],
  "extra": {
    "title": "입금 123,456 원"
  }
}
```



### AT + 이미지, 아이템 리스트

**이미지와 구조화된 목록이 포함된 알림톡**

* 기존 텍스트 알림톡 기본형에 (이미지 / 헤더 / 아이템 하이라이트 / 아이템리스트 / 아이템 요약정보) 5가지 항목이 추가로 구성
* 이미지, 헤더, 아이템 하이라이트 영역을 필요에 따라 1 개 이상 필수 선택하여 템플릿 등록&#x20;
* 템플릿 당 고정된 이미지만 사용 가능
* 아이템리스트는 최소 2개 이상 최대 10개 항목으로 구성 가능 \
  (알림톡 템플릿 강조 유형이 이미지형(IMAGE) 인 경우에만 **msg\_type** 을 **ai** 로 설정해주셔야 발송 가능합니다.) (ex. 알림톡 템플릿 강조 유형이 아이템리스트형이고 이미지가 포함된경우 **msg\_type** 을 **ai** 로 설정시 발송 실패)









**이미지, 아이템리스트형 첨부파일 예시**

**Alimtalk\_image.json (이미지형)**

```json5
{
  "extra": {
    "msg_type": "ai"
  }
}
```

**Alimtalk\_item\_list.json (아이템리스트형, 헤더 + 아이템리스트 + 아이템 요약 정보)**

```json5
{
  "item": {
    "list": [
      {
        "title": "가입일자",
        "description": "2021.5.23"
      },
      {
        "title": "이름",
        "description": "김카카오"
      }
    ],
    "summary": {
      "title": "구매가격",
      "description": "18,000 원"
    }
  },
  "extra": {
    "header": "카카오 가입을 환영합니다."
  }
}
```

**Alimtalk\_item\_list\_button.json ( 아이템리스트형, 버튼 + 이미지 + 아이템 하이라이트 )**

```json5
{
  "button": [
    {
      "name": "채널 추가",
      "type": "AC"
    }
  ],
  "item_highlight": {
    "title": "가입 환영 포인트",
    "description": "10,000P"
  }
}
```



### FT + 이미지

이미지 타입의 친구톡을 발송하기 위하여 반드시 이미지를 사전에 비즈뿌리오 사이트의 **\[카카오톡 비즈메시지] – \[친구톡 이미지 등록]** 을 통해 업로드 해야 합니다. 이후 **\[친구톡 이미지 관리]**에서 해당 이미지 URL 을 확인하셔서 발송합니다.&#x20;

이미지에 대한 정보는 JSON 파일로 만들어 환경설정파일에서 지정한 파일경로(FILE\_PATH)에 JSON 형식 파일을 업로드 한 후, 첨부될 파일은 **ATTACHED\_FILE** 필드에 입력합니다.



**파라미터**

|   키   |     키     |  타입  |  필수 |             설명            |
| :---: | :-------: | :--: | :-: | :-----------------------: |
| image |  img\_url | text |  Y  |           버튼 제목           |
| image | img\_link | text |  N  |      이미지 클릭 시 이동할 URL     |
| extra |    wide   | text |  N  | 와이드 버블 사용 여부 (Y/N, 기본값 N) |



친구톡 + 이미지 타입 첨부파일의 실제 내용은 다음과 같이 JSON 형태로 구성됩니다.

**image.json**

```json5
{
  "image": {
    "img_url": "등록된 이미지 URL",
    "img_link": "http://bizmessage.kakao.com/"
  },
  "extra": {
    "wide": "Y"
  }
}
```



친구톡+버튼링크+이미지타입 첨부파일의 실제 내용은 다음과 같이 하나의 JSON 형태로 구성됩니다.

**button.json**

```json5
{
  "button": [
    {
      "name": "미리 주문하기",
      "type": "WL",
      "url_mobile": "http://www.kakao.com"
    }
  ],
  "image": {
    "img_url": "등록된 이미지 URL",
    "img_link": "http://bizmessage.kakao.com/"
  }
}
```
