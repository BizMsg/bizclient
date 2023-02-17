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

### RCS 공통포맷 (MESSAGEBASE\_ID)

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

> **RCS MMS 슬라이드형(Carousel Medium, Small)은 1,300자까지 발송 가능하나 실제 단말에서 수신 가능한 글자 수가 적어 메시지 내용이 잘려 발송될 수 있습니다.**
>
> **아래 글자/라인수 정의 확인하시어 발송하시기 바랍니다.**&#x20;

> **RCS MMS 슬라이드형 글자/ 라인수 정의**&#x20;
>
> 글자 수 : 1줄 당 정상적으로 표현가능한 글자 수, 한글 **'**가' 기준 측정
>
> 라인 수 : 수신 가능한 디스크립션(본문) 줄 수

****

**LMS (Standalone No Media)**

\[글자 수]

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

\[줄 수(접혀있는 경우)]

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

**MMS (Standalone Media Top - 세로형)**

\[글자 수]

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

\[줄 수(Media Tall인 경우, 접혀있는 경우)]

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

\[줄 수(Media Medium인 경우, 접혀있는 경우)]

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

**MMS (Carousel Medium - 슬라이드)**

<figure><img src="../.gitbook/assets/image (1) (2).png" alt=""><figcaption></figcaption></figure>

![](<../.gitbook/assets/image (15).png>)

**MMS (Carousel Small - 슬라이드형)**

![](<../.gitbook/assets/image (6) (2).png>)

![](<../.gitbook/assets/image (16).png>)



### RCS BODY

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



**신규 RCS 포맷**&#x20;

```json
"body": {
    "title1": "제목",
    "description1": "본문 텍스트",
    "media1": "maapfile://{fileId_1}",
    "title2": "제목 2번째 카드",
    "description2": "본문 텍스트",
    "media2": "maapfile://{fileId_2}",
    "title3": "제목 3번째 카드",
    "description3": "본문 텍스트",
    "media3": "maapfile://{fileId_3}",
    "media": "maapfile://{fileId_main}      > (신규포맷 mms 전용) 상단 main 이미지",
    "title": "제목 텍스트                   > (신규포맷 mms 전용) 상단 main 제목",
    "description": "본문 텍스트             > (신규포맷 mms 전용) 상단 main 본문",
    "subMedia1": "maapfile://{fileId_sub1}  > (신규포맷 mms 전용) 선택 옵션 서브 이미지 1",
    "subMediaUrl1": "URL                    > (신규포맷 mms 전용) 선택 옵션 서브 이미지 1 클릭 시 랜딩 URL",
    "subTitle1": "제목 텍스트               > (신규포맷 mms 전용) 선택 옵션 소제목 1",
    "subDesc1": "본문 텍스트                > (신규포맷 mms 전용) 선택 옵션 소본문 1",
    "subMedia2": "maapfile://{fileId_sub2}  > (신규포맷 mms 전용) 선택 옵션 서브 이미지 2",
    "subMediaUrl2": "URL                    > (신규포맷 mms 전용) 선택 옵션 서브 이미지 2 클릭 시 랜딩 URL",
    "subTitle2": "제목 텍스트               > (신규포맷 mms 전용) 선택 옵션 소제목 2",
    "subDesc2": "본문 텍스트                > (신규포맷 mms 전용) 선택 옵션 소본문 2",
    "subMedia3": "maapfile://{fileId_sub3}  > (신규포맷 mms 전용) 선택 옵션 서브 이미지 3",
    "subMediaUrl3": "URL                    > (신규포맷 mms 전용) 선택 옵션 서브 이미지 3 클릭 시 랜딩 URL",
    "subTitle3": "제목 텍스트               > (신규포맷 mms 전용) 선택 옵션 소제목 3",
    "subDesc3": "본문 텍스트                > (신규포맷 mms 전용) 선택 옵션 소본문 3"
 }
```

****

**media 종류**

**1. 이미지**

* 비즈뿌리오 사이트 \[메시지관리] - \[RCS 관리] - \[RCS 이미지 관리] 에서 이미지를 등록하여 사용합니다. 이미지는 등록일로부터 <mark style="color:orange;">365일간 발송 가능</mark>합니다. (이후 자동 삭제)

> **포맷**&#x20;
>
> maapfile://{fileId}
>
> &#x20;****&#x20;
>
> **예시**&#x20;
>
> "media" : "maapfile://BR.i6dOpSm8N8.20200302150000.001"

#### 2. 동영상 스트리밍

* 3가지 형태의 YouTube URL 주소 지원 (정확한 형식을 준수해야 하며, 일부만 일치하는 경우 실패)
*   동영상 썸네일은 등록된 이미지만 사용 가능하며 YouTube URL 뒤에 콤마(,)와 함께 입력

    (콤마(,) 외 공백을 포함하는 경우 실패)
* 동영상 발송 시 Footer에 '동영상 재생 시 데이터 요금제가 적용됩니다.'라는 문구 자동 삽입

> **포맷**&#x20;
>
> https://www.youtube.com/watch?v=\[videoId],maapfile://{썸네일용 fileId\_1}
>
> https://youtu.be/\[VideoId],maapfile://{썸네일용 fileId\_2}
>
> https://m.youtube.com/watch?v=\[videoId],maapfile://{썸네일용 fileId\_3}
>
> &#x20;
>
> **예시**&#x20;
>
> "media1" : "https://www.youtube.com/watch?v=KCbtF9I0qvI,maapfile://BR.i6dOpSm8N8.20200302150000.001"



### RCS + BUTTONS

RCS 에 버튼 링크를 추가하고자 할 경우 아래와 같은 JSON 형식에 맞춰 RCS 테이블(BIZ\_RCS)의 **BUTTONS** 필드에 입력합니다.

```sql
INSERT INTO biz_msg ( 
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, RCS_REFKEY)

VALUES (
8, '201XXXXXXXXX', NOW(), NOW(), '01012341234', '0212341234', {RCS_REFKEY})
```

#### 버튼 구조 (JSON)

```json5
{
"buttons"
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

버튼 표현 방식 3장의 카드이고 2, 0, 1의 버튼이 있다고 가정하면 BUTTONS는 아래와 같이 구성 할 수 있습니다.\
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

**New RCS examples**

Highlighted image n title (이미지 & 타이틀 강조형)

```json
{
  "body": {
    "media": "maapfile://fileId123", (필수)
    "title": "제목",
    "subTitle1": "소제목1",(필수)
    "subDesc1": "소본문1",(필수)
    "subTitle2": "소제목2",
    "subDesc2": "소본문2"
  },
  "buttons": [
    {
      "suggestions": [
        {
          "action": {
            "urlAction": {
              "openUrl": {
                "url": "https://www.google.com"
              }
            },
            "displayText": "구글"
          }
        },
        {
          "action": {
            "urlAction": {
              "openUrl": {
                "url": "https://www.naver.com"
              }
            },
            "displayText": "네이버"
          }
        }
      ]
    }
  ]
}

```

이미지 강조형, SNS형

```json5
{
  "body": {
    "media": "maapfile://fileId123",(필수)
    "title": "제목",
    "description": "본문"(필수)
  },
  "buttons": [
    {
      "suggestions": [
        {
          "action": {
            "urlAction": {
              "openUrl": {
                "url": "https://www.google.com"
              }
            },
            "displayText": "구글"
          }
        },
        {
          "action": {
            "urlAction": {
              "openUrl": {
                "url": "https://www.naver.com"
              }
            },
            "displayText": "네이버"
          }
        }
      ]
    }
  ]
}

```

썸네일형 (세로)

```json5
{
  "body": {
    "media": "maapfile://fileId123",(필수)
    "title": "제목",
    "description": "본문",
    "subMedia1": "maapfile://fileid456",(필수)
    "subMediaUrl1": "http://www.naver.com",
    "subDesc1": "소본문1 이미지클릭가능",(필수)
    "subMedia2": "maapfile://fileid789",(필수)
    "subDesc2": "소본문2 이미지클릭불가"(필수)
  },
  "buttons": [
    {
      "suggestions": [
        {
          "action": {
            "urlAction": {
              "openUrl": {
                "url": "https://www.google.com"
              }
            },
            "displayText": "구글"
          }
        },
        {
          "action": {
            "urlAction": {
              "openUrl": {
                "url": "https://www.naver.com"
              }
            },
            "displayText": "네이버"
          }
        }
      ]
    }
  ]
}

```

썸네일형 (가로)

```json5
{
  "body": {
    "media": "maapfile://fileId123",(필수)
    "title": "제목",
    "description": "본문",(필수)
    "subMedia1": "maapfile://fileid456",(필수)
    "subMediaUrl1": "http://www.naver.com",
    "subMedia2": "maapfile://fileid789",(필수)
    "subMedia3": "maapfile://fileid000"(필수)
  },
  "buttons": [
    {
      "suggestions": [
        {
          "action": {
            "urlAction": {
              "openUrl": {
                "url": "https://www.google.com"
              }
            },
            "displayText": "구글"
          }
        },
        {
          "action": {
            "urlAction": {
              "openUrl": {
                "url": "https://www.naver.com"
              }
            },
            "displayText": "네이버"
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
