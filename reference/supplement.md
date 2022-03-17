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



### AT/FT ATTACHMENT 정보 및 추가정보









