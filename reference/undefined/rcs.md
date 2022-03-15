# RCS



### RCS

RCS는 비즈뿌리오 서버에 등록된 사용 가능한 챗봇ID와 메시지베이스ID를 사용하여 발송되며 RCS 지원기기 사용자인 경우 발송 가능합니다.

\
메시지베이스 ID 는 이통사에서 제공하는 **메시지 포맷**을 사용하거나 **\[RCS 비즈센터]**을 통해 **템플릿**을 등록하여 사용가능합니다.



```sql
INSERT INTO biz_msg ( 
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, RCS_REFKEY)

VALUES (
8, ‘201XXXXXXXXX’, NOW(), NOW(), ‘01012341234’, ‘0212341234’, , {RCS_REFKEY})
```

****

**BODY**

key : title, media, description

리치카드 개수 및 순서에 따라 넘버링 (ex. title1, title2, ...)

```json5
#1개
{
    “title” : “카드”,
    “media” : “등록된 이미지 URL”, 
    “description”: “안녕하세요!”
}
```

```json5
#2개 이상
{
    “title1” : “카드”,
    “media1” : “등록된 이미지 URL”, 
    “description1”: “안녕하세요!”, 
    “title2” : “카드 2”,
    “media2” : “등록된 이미지 URL”, 
    “description2”: “안녕하세요!”,
            .
            .
            .
}
```





### RCS + BUTTONS

RCS 에 버튼 링크를 추가하고자 할 경우 아래와 같은 JSON 형식에 맞춰 RCS 테이블(BIZ\_RCS)의 BUTTONS 필드에 입력합니다.



```sql
INSERT INTO biz_msg ( 
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, RCS_REFKEY)

VALUES (
8, ‘201XXXXXXXXX’, NOW(), NOW(), ‘01012341234’, ‘0212341234’, {RCS_REFKEY})
```

