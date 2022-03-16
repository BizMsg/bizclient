# FAX

한글 100자 이하의 표지를 포함한 이미지 및 문서를 발송할 수 있습니다.

\*

```sql
INSERT INTO biz_msg (
MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE, SEND_PHONE, 
SUBJECT, MSG_BODY, ATTACHED_FILE, COVER_FLAG)

VALUES (
2, ‘201XXXXXXXXX’, NOW(), NOW(), ‘03112341234’, ‘0212341234’, 
‘표지제목’, ‘표지내용’, {첨부파일}, {팩스표지 사용여부 (사용할 경우 1 입력)})
```

