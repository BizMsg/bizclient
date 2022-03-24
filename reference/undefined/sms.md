# SMS

### SMS (텍스트 90byte 이하의 단문 메시지)

```sql
INSERT INTO biz_msg ( 
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, MSG_BODY)

VALUES (
0, '201XXXXXXXXX', NOW(), NOW(), 
'01012341234', '0212341234', '본 메시지는 SMS 테스트 메시지 입니다.')
```
