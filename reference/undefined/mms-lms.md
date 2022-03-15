# MMS/LMS



### MMS

텍스트 2000byte 이하, 이미지 60kb 이하 등 멀티미디어를 같이 보내는 메시지

```sql
INSERT INTO biz_msg ( 
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, 
DEST_PHONE, SEND_PHONE, SUBJECT, MSG_BODY, ATTACHED_FILE)

VALUES (
5, ‘201XXXXXXXXX’, NOW(), NOW(), ‘01012341234’, ‘0212341234’, 
‘MMS 제목’, ‘본 메시지는 MMS 테스트 메시지 입니다.’, {첨부파일명.jpg})
```



### LMS

텍스트 2000byte 이하의 장문 메시지

```sql
INSERT INTO biz_msg ( 
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, 
DEST_PHONE, SEND_PHONE, SUBJECT, MSG_BODY)
VALUES (
5, ‘201XXXXXXXXX’, NOW(), NOW(), ‘01012341234’, ‘0212341234’, 
‘LMS 제목’, ‘본 메시지는 LMS 테스트 메시지 입니다.’)
```
