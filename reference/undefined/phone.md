# PHONE

### PHONE

한글 100자 이하의 TTS(Text to Speech) 및 3분 미만의 WAVE 파일을 발송할 수 있습니다.

```sql
INSERT INTO biz_msg (MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, DEST_PHONE,
 SEND_PHONE, MSG_BODY, VXML_FILE, REPLY_FLAG)
 
VALUES (3, '201XXXXXXXXX', NOW(), NOW(), '01012341234', '0212341234',
'본 메시지는 테스트입니다. 다우기술 비즈메시지 서비스를 이용해주셔서 감사합니다.', 
{시나리오파일 사용시, 시나리오파일명}, {시나리오 답변 기능 사용여부 (사용할 경우 1 입력)})
```
