# RCS

### RCS

RCS는 비즈뿌리오 서버에 등록된 사용 가능한 **챗봇ID**와 **메시지베이스ID**를 사용하여 발송되며 RCS 지원기기 사용자인 경우 발송 가능합니다.

\
메시지베이스 ID 는 이통사에서 제공하는 **메시지 포맷**을 사용하거나 **RCS 비즈센터**를 통해 **템플릿**을 등록하여 사용가능합니다.

```sql
INSERT INTO biz_msg ( 
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, RCS_REFKEY)

VALUES (
8, '201XXXXXXXXX', NOW(), NOW(), '01012341234', '0212341234', {RCS_REFKEY})
```

***

**BODY**

**key : title, media, description**

리치카드 개수 및 순서에 따라 넘버링 (ex. title1, title2, ...)

```json5
#1개
{
    "title" : "카드",
    "media" : "등록된 이미지 URL", 
    "description": "안녕하세요!"
}
```

```json5
#2개 이상
{
    "title1" : "카드",
    "media1" : "등록된 이미지 URL", 
    "description1": "안녕하세요!", 
    "title2" : "카드 2",
    "media2" : "등록된 이미지 URL", 
    "description2" : "안녕하세요!",
            .
            .
            .
}
```

URL 예시 – maapfile://BR.i6dOpSm8N8.20200302150000.001

### RCS 공통포맷 (MESSAGEBASE\_ID)

| MESSAGEBASE\_ID |  상품 |        메시지 타입        | 카드 장 수 | 최대 버튼 수 | 메시지 최대 본문 길이 (글자수) |
| :-------------: | :-: | :------------------: | :----: | :-----: | :----------------: |
|     SS000000    | SMS |      Standalone      |    1   |    1    |         100        |
|     SL000000    | LMS |      Standalone      |    1   |    3    |        1300        |
|     SMwThT00    | MMS | Standalone Media Top |    1   |    2    |        1300        |
|     SMwThM00    | MMS | Standalone Media Top |    1   |    2    |        1300        |
|    CMwMhM0300   | MMS |    Carousel Medium   |    3   |    2    |     1300 (총 합)     |
|    CMwMhM0400   | MMS |    Carousel Medium   |    4   |    2    |     1300 (총 합)     |
|    CMwMhM0500   | MMS |    Carousel Medium   |    5   |    2    |     1300 (총 합)     |
|    CMwMhM0600   | MMS |    Carousel Medium   |    6   |    2    |     1300 (총 합)     |
|    CMwShS0300   | MMS |    Carousel Small    |    3   |    2    |     1300 (총 합)     |
|    CMwShS0400   | MMS |    Carousel Small    |    4   |    2    |     1300 (총 합)     |
|    CMwShS0500   | MMS |    Carousel Small    |    5   |    2    |     1300 (총 합)     |
|    CMwShS0600   | MMS |    Carousel Small    |    6   |    2    |     1300 (총 합)     |

> RCS MMS 슬라이드형(Carousel Medium, Small)은 1,300 자까지 발송 가능하나\
> 실제 단말에서 수신 가능한 글자 수가 적어 메시지 내용이 잘려 발송될 가능성이 존재합니다.

> 포토여부/타이틀 글자 수/버튼 개수에 따라 입력 가능한 본문 글자 수가 상이할 수 있습니다.

### RCS + BUTTONS

RCS 에 버튼 링크를 추가하고자 할 경우 아래와 같은 JSON 형식에 맞춰 RCS 테이블(BIZ\_RCS)의 **BUTTONS** 필드에 입력합니다.

```sql
INSERT INTO biz_msg ( 
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, RCS_REFKEY)

VALUES (
8, '201XXXXXXXXX', NOW(), NOW(), '01012341234', '0212341234', {RCS_REFKEY})
```

#### 버튼 구조 (JSON)

* [BUTTONS](../supplement.md#buttons)
  * [suggestions](../supplement.md#suggestions)
    * [postback](../supplement.md#postback)
    * [action](../supplement.md#action)
      * [urlAction](../supplement.md#urlaction)
      * [dialerAction](../supplement.md#dialeraction)
      * [mapAction](../supplement.md#mapaction)
      * [mapAction](../supplement.md#mapaction-1)
      * [calendarAction](../supplement.md#calendaraction)
      * [composeAction](../supplement.md#composeaction)
      * [clipboardAction](../supplement.md#clipboardaction)

```json5
{
  "Buttons": [
    {
      "suggestions": [
        {
          "action": {
            "urlAction": {
              "openUrl": {
                "url": {}
              }
            },
            "dialerAction": {
              "dialPhoneNumber": {
                "phoneNumber": {}
              }
            },
            "mapAction": {
              "showLocation": {
                "location": {
                  "query": {},
                  "latitude": {},
                  "longitude": {},
                  "label": {}
                },
                "fallbackUrl": {}
              },
              "requestLocationPush": {}
            },
            "calendarAction": {
              "createCalendarEvent": {
                "startTime": {},
                "endTime": {},
                "title": {},
                "description": {}
              }
            },
            "composeAction": {
              "composeTextMessage": {
                "phoneNumber": {},
                "text": {}
              }
            },
            "clipboardAction": {
              "copyToClipboard": {
                "text": {}
              }
            }
          }
        }
      ]
    }
  ]
}
```

**Action 예시**

버튼 표현 방식 3장의 카드이고 2, 0, 1의 버튼이 있다고 가정하면 \*\*\*\* BUTTONS는 아래와 같이 구성 할 수 있습니다.\
(JSON KEY 대소문자 구분)

```json5
{
  "BUTTONS": [
    {
      "suggestions": [
        {
          "action": {
            "urlAction": {
              "openUrl": {
                "url": "https://www.google.com"
              }
            },
            "displayText": "Open website or deep link",
            "postback": {
              "data": "set_by_chatbot_open_url"
            }
          }
        },
        {
          "action": {
            "urlAction": {
              "openUrl": {
                "url": "https://www.google2.com"
              }
            },
            "displayText": "Open website or deep link",
            "postback": {
              "data": "set_by_chatbot_open_url_2"
            }
          }
        }
      ]
    },
    {},
    {
      "suggestions": [
        {
          "action": {
            "urlAction": {
              "openUrl": {
                "url": "https://www.google2.com"
              }
            },
            "displayText": "Open website or deep link",
            "postback": {
              "data": "set_by_chatbot_open_url_2"
            }
          }
        }
      ]
    }
  ]
}
```

### 대체 발송 타입 (RE\_TYPE)

1차 대체발송 타입에 따라 최대 2 차 대체발송까지 가능합니다.

| 1차 대체 발송 | 2차 대체 발송 | RE\_TYPE 입력값 |
| :------: | :------: | :----------: |
|    SMS   |          |      SMS     |
|    MMS   |          |      MMS     |
|    AT    |          |       K      |
|    AT    |    SMS   |      KS      |
|    AT    |    MMS   |      KM      |
|    FT    |          |              |
|    FT    |    SMS   |      BS      |
|    FT    |    MMS   |      BM      |
|    BI    |          |       I      |
|    BI    |    SMS   |      IS      |
|    BI    |    MMS   |      IM      |
|    BW    |          |       W      |
|    BW    |    SMS   |      WS      |
|    BW    |    MMS   |      WM      |

### RCS + 1차 대체 발송

RCS 결과 실패 시 지정하신 대체발송타입(SMS/MMS/AT/FT)과 대체발송본문을 사용하여 발송됩니다.\
(단, 비즈뿌리오 ID 가 대체 발송 사용 가능하도록 설정되어 있어야 합니다.)\
(SMS 대체발송의 경우에는 메시지 본문 (RE\_BODY) 길이가 SMS 의 허용 길이를 초과하였을 때 발송되지 않습니다.)

**RCS + SMS**

```sql
INSERT INTO biz_msg ( 
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, 
DEST_PHONE, SEND_PHONE, RCS_REFKEY, RE_TYPE, RE_BODY)

VALUES (
8, '201XXXXXXXXX', NOW(), NOW(), '01012341234', '0212341234', 
{RCS_REFKEY}, 'SMS', '[다우기술] 응모하신 프로모션에 당첨되셨습니다.')
```

**RCS + MMS**

```sql
INSERT INTO biz_msg ( 
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, 
DEST_PHONE, SEND_PHONE, RCS_REFKEY, RE_TYPE, RE_BODY, ATTACHED_FILE)

VALUES (
8, '201XXXXXXXXX', NOW(), NOW(), '01012341234', '0212341234',
{RCS_REFKEY}, 'MMS', '[다우기술] 응모하신 프로모션에 당첨되셨습니다.', '{첨부파일.jpg}')
```

아래의 알림톡/친구톡으로 대체 발송 하는 경우 **MSG\_BODY** 필드의 데이터를 사용하여 발송됩니다.

**RCS + AT**

```sql
INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, 
MSG_BODY, TEMPLATE_CODE, SENDER_KEY, NATION_CODE, RE_TYPE, RCS_REFKEY)

VALUES (
8, '201XXXXXXXXX', NOW(), NOW(), '01012341234', '0212341234',
'홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.', {템플릿코드}, {발신프로필키},
'82', 'K', '{RCS_REFKEY}')
```

**RCS + FT**

```sql
INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, 
MSG_BODY, SENDER_KEY, NATION_CODE, RE_TYPE, RCS_REFKEY)

VALUES (
8, '201XXXXXXXXX', NOW(), NOW(), '01012341234', '0212341234',
'홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.', {발신프로필키}, 
'82', 'B', '{RCS_REFKEY}')
```

> 대체 발송이 이루어진 경우, 클라이언트는 수신 받은 리포트를 업데이트하는 시점에 대체 발송에 대한 정보를 추가 레코드로 신규 생성하게 됩니다.\
> RCS 와 대체 발송에 대한 레코드의 매핑 키는 알림톡/친구톡의 **UMID** 필드가 대체 발송의 **CMID** 필드로 이루어집니다.

### RCS + 2차 대체 발송

RCS 결과 실패 시 지정하신 1 차 대체 발송 타입(AT/FT)을 발송하며 알림톡/친구톡 발송 결과 실패 시 지정하신 2 차 대체 발송 타입(SMS/MMS)과 대체 발송 본문을 사용하여 발송됩니다.\
\
알림톡/친구톡 대체 발송의 경우 **MSG\_BODY** 필드의 데이터를 사용하여 발송되며 SMS/MMS 대체 발송의 경우 대체 발송 본문에 대해 알림톡/친구톡과 동일 본문(MSG\_BODY)을 사용하려면, 대체 발송 메시지 필드(RE\_BODY)를 비워두시면 됩니다.

단, 비즈뿌리오 ID 가 대체 발송 사용 가능하도록 설정되어 있어야 합니다.\
SMS 대체발송의 경우에는 메시지 본문 (MSG\_BODY) 길이가 SMS 의 허용 길이를 초과하였을 때 발송되지 않습니다.

알림톡/친구톡 대체 발송의 경우 **MSG\_BODY** 필드의 데이터를 사용하여 발송됩니다.

**RCS + AT(1차) + SMS(2차)**

```sql
INSERT INTO biz_msg ( 
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, 
RCS_REFKEY, RE_TYPE, MSG_BODY,TEMPLATE_CODE, SENDER_KEY, NATION_CODE, RE_BODY ) 

VALUES (
8, '201XXXXXXXXX', NOW(), NOW(), '01012341234', '0212341234',
{RCS_REFKEY}, 'KS', ' 홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.', 
{템플릿코드}, {발신프로필키}, '82', '[다우기술] 응모하신 프로모션에 당첨되셨습니다.')
```

**RCS + AT(1차) + SMS(2차)**

```sql
INSERT INTO biz_msg ( 
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, 
RCS_REFKEY, RE_TYPE, MSG_BODY, TEMPLATE_CODE, SENDER_KEY, NATION_CODE, RE_BODY,
ATTACHED_FILE )

VALUES (
8, '201XXXXXXXXX', NOW(), NOW(), '01012341234', '0212341234',
{RCS_REFKEY}, 'KM', ' 홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.', 
{템플릿코드}, {발신프로필키}, '82', '[다우기술] 응모하신 프로모션에 당첨되셨습니다.', {첨부파일.jpg})
```

**RCS + FT(1차) + SMS(2차)**

```sql
INSERT INTO biz_msg ( 
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, 
RCS_REFKEY, RE_TYPE, MSG_BODY, SENDER_KEY, NATION_CODE, RE_BODY )

VALUES (8, ‘201XXXXXXXXX’, NOW(), NOW(), ‘01012341234’, ‘0212341234’,
{RCS_REFKEY}, ‘BS’, ‘ 홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.’, 
{발신프로필키}, ‘82’, ‘[다우기술] 응모하신 프로모션에 당첨되셨습니다.’)
```

**RCS + FT(1차) + SMS(2차)**

```sql
INSERT INTO biz_msg ( 
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, 
RCS_REFKEY, RE_TYPE, MSG_BODY, SENDER_KEY, NATION_CODE, RE_BODY, ATTACHED_FILE )

VALUES (8,'201XXXXXXXXX', NOW(), NOW(), '01012341234', '0212341234',
{RCS_REFKEY}, 'BM', ' 홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.', 
{발신프로필키}, '82', '[다우기술] 응모하신 프로모션에 당첨되셨습니다.', {첨부파일.jpg})
```

> 대체 발송이 이루어진 경우, 클라이언트는 수신 받은 리포트를 업데이트하는 시점에 대체 발송에 대한 정보를 추가 레코드로 신규 생성하게 됩니다.\
> RCS 와 대체 발송에 대한 레코드의 매핑 키는 RCS 의 **UMID** 필드가 대체 발송의 **CMID** 필드로 이루어집니다.

> 2차 대체 발송이 이루어진 경우, RCS의 **UMID**값 앞에 "\*\*RE\_"\*\*이 추가된 문자열이 2차 대체발송의 **CMID** 필드로 이루어지며 1차 대체발송의 **UMID** 도 같은 값으로 설정됩니다..
