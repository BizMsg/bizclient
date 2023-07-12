---
description: 알림톡/친구톡
---

# 카카오톡 비즈메시지

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

친구톡은 비즈뿌리오 서버에 등록된 사용 가능한 **발신 프로필 키**를 사용하여 발송되며, 카카오톡 사용자이고 발신 프로필(카카오톡 채널)과 **친구일 경우** 발송 가능합니다.

> 친구톡은 한글, 영어, 숫자, 특수문자 및 공백을 모두 포함하여 최대 1000 자 까지만 발송 가능합니다.

```sql
INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, 
DEST_PHONE, SEND_PHONE, MSG_BODY, SENDER_KEY, NATION_CODE)

VALUES (
6, '201XXXXXXXXX', NOW(), NOW(), '01012341234', '0212341234',
'홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.', {발신프로필키}, '82'
```

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

> 대체 발송이 이루어진 경우, 클라이언트는 수신 받은 리포트를 업데이트하는 시점에 대체 발송에 대한 정보를 추가 레코드로 신규 생성하게 됩니다.\
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

> 2차 대체 발송이 이루어진 경우, 알림톡/친구톡의 **UMID** 값 앞에 "\*\*RE\_"\*\*이 추가된 문자열이 2차 대체 발송의 **CMID** 필드로 이루어지며 1차 대체 발송의 **UMID** 도 같은 값으로 설정됩니다.

### AT/FT + ATTACHMENT 발송

알림톡/친구톡에 버튼 및 추가 기능을 사용하고자 할 경우 환경설정 파일에서 지정한 파일경로(FILE\_PATH)에 JSON 형식 파일을 업로드 한 후, 첨부될 파일은 **ATTACHED\_FILE** 필드에 입력합니다.

(JSON 형식 파일 인코딩은 **EUC-KR** 로 생성되어 있어야 합니다.)

\
(웹 링크, 앱 링크에 변수가 있거나 JSON 파일 생성이 어려운 경우 **FILE\_HANDLING\_MODE** 테이블을 활용 할 수 있습니다.)

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



### AT/FT ATTACHMENT 정보

Key:supplement 항목은 아래 이어지는 supplement 테이블을 참고

![](<../.gitbook/assets/image (8) (1).png>)

**supplement**

![](<../.gitbook/assets/image (6) (1) (1).png>)

### **AT/FT + BUTTON**

**버튼 타입**

![](<../.gitbook/assets/image (4) (2).png>)

#### AT/FT + 버튼 타입별 속성

![](<../.gitbook/assets/image (9) (1) (1).png>)

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



### **AT + 바로연결**

알림톡 바로연결이란?

* 알림톡 하단에 가로 슬라이드 형태로 표시되며 웹/앱 연결, 상담톡 전환 등을 호출하는 기능
* 상담톡 또는 챗봇을 사용하는 발신프로필만 이용 가능
* 바로연결은 최대 10개까지 사용 가능, 사용 시 버튼 개수는 2개로 제한\
  \*(챗봇, 상담톡 사용 채널에만 한해 사용 가능합니다.)

#### AT + 바로연결 타입별 속성

![](<../.gitbook/assets/image (7) (3).png>)

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
* 이미지, 헤더, 아이템 하이라이트 영역을 필요에 따라 1 개 이상 필수 선택하여 템플릿 등록
* 템플릿 당 고정된 이미지만 사용 가능
* 아이템리스트는 최소 2개 이상 최대 10개 항목으로 구성 가능\
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

이미지 타입의 친구톡을 발송하기 위하여 반드시 이미지를 사전에 비즈뿌리오 사이트의 **\[카카오톡 비즈메시지] – \[친구톡 이미지 등록]** 을 통해 업로드 해야 합니다. 이후 **\*\[친구톡 이미지 관리]**에서 해당 이미지 URL 을 확인하여 발송합니다.

이미지에 대한 정보는 JSON 파일로 만들어 환경설정 파일에서 지정한 파일경로(FILE\_PATH)에 JSON 형식 파일을 업로드 한 후, 첨부될 파일은 **ATTACHED\_FILE** 필드에 입력합니다.

**파라미터**

![](<../.gitbook/assets/image (9) (1).png>)

친구톡 + 이미지 타입 첨부파일의 실제 내용은 다음과 같이 JSON 형태로 구성됩니다.

**image.json**

```json5
{
  "image": {
    "img_url": "등록된 이미지 URL",
    "img_link": "http://bizmessage.kakao.com/"
  },
  "extra": {
    "wide": "Y" //와이드형 이미지일경우에만 기재
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



### 카카오톡 이모티콘 삽입

카카오톡 기본 이모티콘 삽입을 원할 경우 이모티콘에 해당하는 명령어를 입력합니다.

예) 안녕하세요 (하하)(씨익)

<figure><img src="../.gitbook/assets/카카오톡 이모티콘 이름 (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
카카오에서 공식적으로 지원하는 기능이 아니므로 명령어에 대한 변경이 있을 수 있습니다.
{% endhint %}

