# Table Schema





### 비즈클라이언트 테이블 구조

비즈클라이언트에서 사용하는 테이블의 목록은 다음과 같으며, \
테이블 생성 권한만 있다면, 자동으로 해당 테이블들을 생성합니다.

> 메시지 테이블 : **BIZ\_MSG**
>
> * 메시지 발송을 위한 데이터가 입력되며, 발송결과업데이트가 이루어지기까지 데이터가 존재하는 테이블

> 로그 테이블 – **BIZ\_LOG\_YYYYMM**&#x20;
>
> * 메시지 테이블에서 발송 결과 업데이트가 완료된 데이터가 이동되는 테이

\


테이블의 각 컬럼은 다음과 같습니다.

_\*표시 컬럼은 비즈클라이언트에서 사용_

|       컬럼 명       |       필수입력 여부       | Y/N | 기본값 |   타입   |  길이  |                                                설명                                               |
| :--------------: | :-----------------: | :-: | :-: | :----: | :--: | :---------------------------------------------------------------------------------------------: |
|       CMID       |          공통         |  Y  |     | String |  32  |                      <p>데이터 ID, 고유한 값</p><p>MSG_TABLE 일 경우 Primary Key</p>                      |
|       UMID       |          공통         |  N  |     | String |  32  |                                    비즈뿌리오 서버에서 정의한 MESSAGE ID                                    |
|     MSG\_TYPE    |          공통         |  Y  |  0  |        |   1  |                 데이터 타입 (SMS 0/FAX 2/PHONE 3 /MMS 5/AT 6/FT 7/RCS 8/BI 11/BW 12)                 |
|      STATUS      |          공통         |  Y  |  0  |        |   1  |                                  데이터 발송 상태 (대기 0/발송중 1/발송완료 2)                                  |
|   REQUEST\_TIME  |          공통         |  Y  | now |        |      |                                            데이터 등록 시간                                            |
|    SEND\_TIME    |          공통         |  Y  | now |        |      |                                             발송 기준 시간                                            |
|   REPORT\_TIME   |          공통         |  N  |     |        |      |                                            단말기 수신 시간                                            |
|    DEST\_PHONE   |          공통         |  Y  |     | String |  16  |                                               수신번호                                              |
|    DEST\_NAME    |          공통         |  N  |     | String |  32  |                                               수신자명                                              |
|    SEND\_PHONE   |          공통         |  Y  |     | String |  16  |                                              발신자번호                                              |
|    SEND\_NAME    |          공통         |  N  |     | String |  32  |                                               발신자명                                              |
|      SUBJECT     |       FAX/MMS       |  N  |     | String |  64  |                                                제                                                |
|     MSG\_BODY    |          공통         |  Y  |     | String | 2000 |                                              메시지 내용                                             |
|   NATION\_CODE   |     AT/FT/BI/BW     |  Y  |     | String |   5  |                                               국가코드                                              |
|    SENDER\_KEY   |     AT/FT/BI/BW     |  Y  |     | String |  40  |                                             발신프로필 키                                             |
|  TEMPLATE\_CODE  |     AT/FT/BI/BW     |  Y  |     | String |  64  |                                              템플릿 코드                                             |
| RESPONSE\_METHOD |          AT         |  N  |     | String |   8  |                                           발송 방식 (PUSH)                                          |
|      TIMEOUT     |        AT/FT        |  N  |     | String |   4  |                                        대체발송을 위한 타임아웃 시간설정                                       |
|     RE\_TYPE     |        AT/FT        |  N  |     | String |   3  |                                   대체발송 메시지 타입 \*5.4 대체발송타입 참조                                   |
|     RE\_BODY     |   AT/FT/BI/BW/RCS   |  N  |     | String | 2000 |                                           대체발송 메시지 내용                                           |
|     RE\_PART     |   AT/FT/BI/BW/RCS   |  N  |     | String |   1  |                                 대체발송 처리 주체 (C:CLIENT, S:Server)                                 |
|    COVER\_FLAG   |         FAX         |  N  |  0  | Number |   1  |                                             표지 발송 옵션                                            |
|     SMS\_FLAG    |        PHONE        |  N  |  0  | Number |   1  |                                          실패 시 문자 전송 옵션                                          |
|    REPLY\_FLAG   |        PHONE        |  N  |  0  | Number |   1  |                                      시나리오 답변기능 여부(Y:1, N:0)                                     |
|    RETRY\_CNT    |      FAX/PHONE      |  N  |     | Number |   4  |                                              재시도회수                                              |
|  ATTACHED\_FILE  | MMS/FAX/PHONE/AT/FT |  N  |     | String | 1000 | <p>[기본 MODE ] <br>첨부파일 전송 시 파일명 (여러 개일 경우, ‘|’ 문자로 구분)<br>[첨부파일 테이블 MODE ] <br>첨부파일 테이블 KEY</p> |
|    VXML\_FILE    |        PHONE        |  N  |     | String |  64  |                                          음성 시나리오 파일 이름                                          |
|   CALL\_STATUS   |          공통         |  N  |     | String |   4  |                                             발송결과 리포트                                            |
|     USE\_PAGE    |         FAX         |  N  |  0  | Number |   2  |                                             발송 페이지 수                                            |
|     USE\_TIME    |        PHONE        |  N  |  0  | Number |   4  |                                         발송 소요 시간 (단위:초)                                         |
|    SN\_RESULT    |        PHONE        |  N  |  0  | Number |   1  |                                        설문 조사 응답 값 (0\~9)                                        |
|     TEL\_INFO    |          공통         |  N  |     | String |  10  |                                     통신사 정보 (SKT/KTF/LGT/KKO)                                    |
|       CINFO      |          공통         |  N  |     | String |  32  |                           Client Indexed Info 특수기호 (/:\*?”<>\|.) 사용불가                           |
|     USER\_KEY    |          FT         |  N  |     | String |  30  |                                  옐로아이디 봇을 이용해 받은 옐로아이디 사용자 식별키                                  |
|     AD\_FLAG     |          FT         |  N  |     | String |   1  |                              광고성 메시지 필수 표기 사항을 노출 (노출여부 Y/N, 기본값 Y)                             |
|    RCS\_REFKEY   |         RCS         |  N  |     | String |  32  |                                           RCS 테이블 KEY                                           |







### MESSAGE\_SUPPORT\_TYPE

RCS 발송 테이블 설

{% hint style="info" %}
MESSAGE\_SUPPORT\_TYPE 의 기본값은 RCS 발송이 제외되어 있으므로 RCS 발송을 위해서는 uds.conf 파일에 MESSAGE\_SUPPORT\_TYPE = ALL 설정을 추가 해주시기 바랍니다.
{% endhint %}

> RCS 메시지 테이블 : BIZ\_RCS
>
> * RCS 메시지 발송을 위한 데이터가 입력되며, 메시지 테이블의 발송 결과 업데이트가 이루어지기까지
>
> 데이터가 존재하는 테이블

{% hint style="info" %}
RCS\_BACKUP\_OPTION(Y/N, default N)을 사용하지 않으면 \
RCS 메시지 테이블의 데이터를 재사용 할 수 있습니다.
{% endhint %}

|       컬럼 명      | 필수입력 여부 |   타입   |  길이  |                                           설명                                           |
| :-------------: | :-----: | :----: | :--: | :------------------------------------------------------------------------------------: |
|      REFKEY     |    Y    | String |  32  |                     <p>테이블 참조키</p><p>MSG_TABLE 일 경우 Primary Key</p>                    |
|   CHATBOT\_ID   |    Y    | String |  40  |                                 RCS 비즈센터를 통해 생성한 챗봇 ID                                 |
|      HEADER     |    Y    | String |   1  |                            메시지 상단에 식별 문구를 입력 (0:Web 발신,1:광고)                           |
|      FOOTER     |    N    | String |  64  |                                  메시지 하단에 수신 거부 문구를 입력.                                 |
| MESSAGEBASE\_ID |    Y    | String |  40  | <p>RCS 공통포맷 또는 템플릿 ID <br>(RCS SMS, LMS, MMS 공통포맷, 템플릿은 별도등록) <br>*5.5RCS 공통 포맷 참조</p> |
|  COPY\_ALLOWED  |    N    | String |   1  |                      단말기에서 사용자에게 ‘복사’/’공유’ 메뉴 보기 여부 (Y / N, 기본 N)                      |
|    RCS\_BODY    |    Y    | String | 2000 |                             메시지 베이스에서 치환할 파라미터 정보 (Json 형식)                            |
|     BUTTONS     |    N    | String | 2000 |                                메시지에 삽입할 버튼 정보 (Json 형식)                                |

****

****

****

****

### FILE\_HANDLING\_MODE

> 첨부파일 테이블 : **BIZ\_ATTACHMENTS**
>
> * 메시지 발송을 위한 첨부파일 데이터가 입력되는 테이

> 첨부파일 로그 테이블 : **BIZ\_ATTACHMENTS\_LOG\_YYYYMM**
>
> * 첨부파일 테이블에서 발송 결과 업데이트가 완료된 데이터가 이동되는 테이블

{% hint style="info" %}
ATTACHMENTS\_BACKUP\_OPTION(Y/N, default N)을 사용하지 않으면

첨부파일 테이블의 데이터를 재사용 할 수 있습니다.
{% endhint %}

|   컬럼 명   | 필수입력 여부 |  기본값 |   타입   |  길이  |               설명               |     |
| :------: | :-----: | :--: | :----: | :--: | :----------------------------: | :-: |
| MSG\_KEY |    Y    |      | String |  32  |     MSG\_TABLE 과 매칭되는 KEY 값    | 복합키 |
|    SEQ   |    Y    |      | Number |      |             데이터 시퀀스            | 복합키 |
|   TYPE   |    Y    | FILE | String |  10  |   데이터 타입 (FILE / HTTP / JSON)  |     |
| CONTENTS |    Y    |      | String | 2000 | 데이터 값 (파일명 / URL / JSONString) |     |
|          |         |      |        |      |                                |     |
|          |         |      |        |      |                                |     |