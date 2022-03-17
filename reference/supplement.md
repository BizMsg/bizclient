# Supplement



### BUTTONS

|      키      |   타입  |  필수 |
| :---------: | :---: | :-: |
| suggestions | Array |  N  |



### Suggestions

|    키   |   타입   |  필수 |
| :----: | :----: | :-: |
| action | Object |  Y  |



### action

|       키      |   타입   |  필수 |      설명     |
| :----------: | :----: | :-: | :---------: |
| \[action 타입] | Object |  Y  |             |
|  displayText |        |  Y  | 버튼에 출력될 텍스트 |
|   postback   |        |  N  |             |



### postback

|   키  |  필수 |
| :--: | :-: |
| data |  Y  |



### urlAction

|    필드 1   |   필드 2  | 필드 3 |   설명  |
| :-------: | :-----: | :--: | :---: |
| urlAction |         |      | URL 연 |
|           | openUrl |      |       |
|           |         |  url |       |



### dialerAction



|     필드 1     |       필드 2      |     필드 3    |  설명  |
| :----------: | :-------------: | :---------: | :--: |
| dialerAction |                 |             | 전화 걸 |
|              | dialPhoneNumber |             |      |
|              |                 | phoneNumber |      |



### mapAction

|    필드 1   |     필드 2     |     필드 3    |    필드 4   |   설명   |
| :-------: | :----------: | :---------: | :-------: | :----: |
| mapAction |              |             |           | 지도 보여주 |
|           | showLocation |             |           |        |
|           |              |   location  |   query   |        |
|           |              |             |  latitude |        |
|           |              |             | longitude |        |
|           |              |             |   label   |        |
|           |              | fallbackUrl |           |        |



### mapAction

|    필드 1   |         필드 2        |    설명   |
| :-------: | :-----------------: | :-----: |
| mapAction |                     | 현재 위치 공 |
|           | requestLocationPush |         |



### calendarAction

|      필드 1      |         필드 2        |     필드 3    |   설명  |
| :------------: | :-----------------: | :---------: | :---: |
| calendarAction |                     |             | 캘린더 등 |
|                | createCalendarEvent |             |       |
|                |                     |  startTime  |       |
|                |                     |   endTime   |       |
|                |                     |    title    |       |
|                |                     | description |       |



### composeAction

|      필드 1     |        필드 2        |     필드 3    |   설명  |
| :-----------: | :----------------: | :---------: | :---: |
| composeAction |                    |             | 메시지 전 |
|               | composeTextMessage |             |       |
|               |                    | phoneNumber |       |
|               |                    |     text    |       |



### clipboardAction

|       필드 1      |       필드 2      | 필드 3 |  설명 |
| :-------------: | :-------------: | :--: | :-: |
| clipboardAction |                 |      | 복사하 |
|                 | copyToClipboard |      |     |
|                 |                 | text |     |



### 지원 가능한 첨부파일 타입

{% tabs %}
{% tab title="MMS" %}
Image : jpg

Audio : ma3

Video : k3g



_Image 를 제외한 타입에 대해서는, 전송은 되지만 일부 이동통신사 또는 단말기에 대해 지원하지 않을 수 있습니다._
{% endtab %}

{% tab title="AT/FT" %}
Button/Image : JSON
{% endtab %}

{% tab title="PHONE" %}
Voice : wav (8bit-8KHz mono 형식)
{% endtab %}

{% tab title="FAX" %}
Docs : doc, docx, xls, xlsx, ppt, pptx, hwp, pdf, txt, html, html&#x20;

Image : bmp, gif, jpg, png
{% endtab %}
{% endtabs %}



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

{% hint style="warning" %}
필수 파라미터가 아닌 것이 포함된 경우 불필요한 파라미터 입력 에러로 발송이 실패할 수 있습니다.
{% endhint %}



### AT/FT ATTACHMENT 정보



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



