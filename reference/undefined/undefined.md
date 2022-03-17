# 카카오 비즈 메시지





### AT 발송

알림톡은 비즈뿌리오 서버에 등록된 사용 가능한 발신프로필 키와 템플릿코드를 사용하여 발송됩니다.\
(알림톡은 변수 내용을 포함하고 한글, 영어, 숫자, 특수문자 및 공백을 모두 포함하여 최대 1000 자 까지만 발송 가능합니다.)

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

(친구톡은 한글, 영어, 숫자, 특수문자 및 공백을 모두 포함하여 최대 1000 자 까지만 발송 가능합니다.)

```sql
INSERT INTO biz_msg (MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, 
DEST_PHONE, SEND_PHONE, MSG_BODY, TEMPLATE_CODE, SENDER_KEY, NATION_CODE)

VALUES (6, ‘201XXXXXXXXX’, NOW(), NOW(), ‘01012341234’, ‘0212341234’,
‘홍길동 고객님 다우기술 비즈메시지 프로모션에 당첨 되었습니다.’, {템플릿코드}, {발신프로필키}, ‘82’
```



### BI/BW (고정형) 발송

브랜드톡(고정형)은 비즈뿌리오 서버에 등록된 사용 가능한 발신프로필 키와 템플릿코드를 사용하여 발송되며

발신 프로필(옐로우아이디 또는 플러스 친구)과 친구 여부에 따라 전송되는 말풍선이 모양이 달라집니다. \
\* 템플릿 등록 시 텍스트 메시지, 링크 버튼, 이미지(일반, 와이드)를 등록하여 사용 가능합니다.\
(단, 발송하는 MSG\_TYPE 과 TEMPLATE\_CODE 의 이미지 타입이 다르다면 발송이 되지 않습니다.)

```sql
INSERT INTO biz_msg (MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, 
DEST_PHONE, SEND_PHONE, TEMPLATE_CODE, SENDER_KEY, NATION_CODE)

VALUES (11, ‘201XXXXXXXXX’, NOW(), NOW(), 
‘01012341234’, ‘0212341234’, {템플릿코드}, {발신프로필키}, ‘82’)
```

```sql
INSERT INTO biz_msg (MSG_TYPE, CMID, REQUEST_TIME, SEND_TIME, 
DEST_PHONE, SEND_PHONE, TEMPLATE_CODE, SENDER_KEY, NATION_CODE)

VALUES (12, ‘201XXXXXXXXX’, NOW(), NOW(), 
‘01012341234’, ‘0212341234’, {템플릿코드}, {발신프로필키}, ‘82’)
```
