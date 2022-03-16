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
