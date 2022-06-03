# 메시지 전송

메시지 문자열은 **KSC 5601**(ISO 10646-1/Unicode1.1) 한글 코드에 정의된 문자열입니다.

> 이동통신 3사에서 지원하는 인코딩 방식이며 해당 인코딩 범주를 벗어나는 문자는 **?** 로 표시되어 전송 될 수 있습니다.\
> Ex ) 핳, 힣, 탙 ... ...

> **CMID** 는 발송데이터의 고유한 키 값(Primary key)으로서 중복되지 않게 생성해주시면 됩니다.

### 메시지 타입(MSG\_TYPE)

사용자는 총 9가지 (SMS/MMS/AT/FT/BI/BW/RCS/PHONE/FAX)의 메시지 타입 발송이 가능합니다.\
(사전에 비즈 아이디의 서비스 형태가 관련 메시지타입 발송이 가능하도록 설정이 필요)

### 발송 상태 변화(STATUS)

STATUS는 다음과 같은 상태 변화를 가집니다.

|                 코드                |                  내용                 |
| :-------------------------------: | :---------------------------------: |
| <mark style="color:red;">0</mark> |                발송 대기                |
|                 7                 |                 발송 중                |
| <mark style="color:red;">1</mark> |              발송 후 결과 대기             |
| <mark style="color:red;">2</mark> | <p>발송 결과 업데이트<br>(로그 테이블 이동 대상)</p> |
|                 3                 |             리포트 재요청 후 대기            |
|                 11                |           클라이언트 대체발송 처리 중           |
|                 13                |       대체발송 설정을 하지 않고 대체발송 한 경우      |

> **status = 13** 인 경우 로그테이블로 이동되지 않습니다.\
> 대체발송을 사용하시려면 대체발송 사용여부를 변경해주시기 바랍니다.

### 발송 결과 확인(CALL\_STATUS)

발송 결과는 메시지 테이블의 CALL\_STATUS 컬럼으로 확인이 가능하며 **발송 결과 코드**의 상세 설명은 [발송결과코드](../result-code/) 항목을 참고하여 주시기 바랍니다.

### 대체 발송 타입(RE\_TYPE)

사용자는 메시지 타입(AT/FT/BI/BW/RCS)에 따라 최대 2 차 대체발송까지 가능합니다.

상세 설명은 [카카오 비즈 메시지 대체발송](kakao-biz.md#re\_type) \~ [RCS 대체발송](rcs.md#re\_type) 항목을 참고하여 주시기 바랍니다.

### 참고

> 2개 이상의 파일을 전송할 때는 **ATTACHED\_FILE** 필드에 파일 1\*\*|**파일 2**|\*\* ... 형식으로 파일을 **|**(파이프라인) 으로 구분하여 입력합니다 (SMS 제외)&#x20;

> 메시지 타입 별 첨부파일을 발송해야 하는 경우 아래 **지원 가능한 첨부파일 타입**을 참조해주시길 바랍니다.

{% hint style="info" %}
이 후 발송 타입별 샘플 Query는 MySQL 기준으로 작성되었습니다
{% endhint %}



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
Docs : doc, docx, xls, xlsx, ppt, pptx, hwp, pdf, txt, html, html

Image : bmp, gif, jpg, png
{% endtab %}
{% endtabs %}
