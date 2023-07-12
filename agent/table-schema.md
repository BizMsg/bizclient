# Table Schema

### 비즈클라이언트 테이블 구조

비즈클라이언트에서 사용하는 테이블의 목록은 다음과 같으며,\
테이블 생성 권한만 있다면, 자동으로 해당 테이블들을 생성합니다.

> 메시지 테이블 : **BIZ\_MSG**
>
> * 메시지 발송을 위한 데이터가 입력되며, 발송 결과 업데이트가 이루어지기까지 데이터가 존재하는 테이블

> 로그 테이블 – **BIZ\_LOG\_YYYYMM**
>
> * 메시지 테이블에서 발송 결과 업데이트가 완료된 데이터가 이동되는 테이블

테이블의 각 컬럼은 다음과 같습니다.

_\*표시 컬럼은 비즈클라이언트에서 사용_

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

> 추가적인 인덱스는 필요에 따라 설정하여 사용하시면 됩니다.
>
> 메시지 테이블의 **CMID** 컬은 **Primary Key** 로 잡혀 있으며, 로그테이블은 중복된 키 값을 허용할 수 있도록 PK가 잡혀있지 않습니다.\
> 참고로, CMID 컬럼이 중복 될 경우 데이터 발송에는 문제가 없으나 결과 리포트 반영이 정상적으로 이루어지지 않을 수 있습니다.

> **CINFO** 컬럼은 고객 회사 내에서 구분이 필요할 경우 (예를 들어 발송하는 데이터에 대해 A 팀, B 팀 등으로 구분하고 싶을 때) 해당 정보 값을 넣어서 발송하면 비즈 뿌리오 서버에서 구분이 되어 데이터가 전송 되며, biz.ppurio.com 의 _**\***_**\[서비스 조회 – 발송 조회]**에서 SUB ID 에 해당 **CINFO** 값이 표시가 됩니다.



### CMID\_ASCII\_CHAR

CMID 필드에 ASCII 범위 외의 문자를 사용하길 희망하는 경우 사용하는 옵션

> CMID 필드는 기본 ASCII 범위의 문자열만 입력 가능합니다.
>
> * &#x20;Y (DEFAULT): ASCII 문자로 구성된 CMID 만 사용 가능합니다.
> *   &#x20;N: ASCII 범위 외 한글 및 특수문자를 포함하려는 경우 사용합니다.
>
>     **\* 주의사항 \***\
>     \- 허용 불가한 CMID 가 입력될 경우에는 발송이 실패할 수 있습니다.



### MESSAGE\_SUPPORT\_TYPE

MESSAGE\_SUPPORT\_TYPE 설정에 따라 RCS 발송에 사용하는 테이블을 생성합니다.

{% hint style="info" %}
MESSAGE\_SUPPORT\_TYPE 의 기본값은 RCS 발송이 제외되어 있으므로 RCS 발송을 위해서는 uds.conf 파일에 MESSAGE\_SUPPORT\_TYPE = ALL 설정을 추가 해주시기 바랍니다.
{% endhint %}

> RCS 메시지 테이블 : BIZ\_RCS
>
> * RCS 메시지 발송을 위한 데이터가 입력되며, 메시지 테이블의 발송 결과 업데이트가 이루어지기까지 데이터가 존재하는 테이블

> RCS 로그 테이블 – BIZ\_RCS\_LOG\_YYYYMM
>
> * RCS 메시지 테이블에서 발송 결과 업데이트가 완료된 데이터가 이동되는 테이블

{% hint style="info" %}
RCS\_BACKUP\_OPTION(Y/N, default N)을 사용하지 않으면\
RCS 메시지 테이블의 데이터를 재사용 할 수 있습니다.
{% endhint %}

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
AGENCY\_ID(대행사 ID) 사용 시 [RCS AGENCY\_ID(대행사 ID)](../appendix.md#rcs-agency\_id-id) 설정 참고
{% endhint %}

***

### FILE\_HANDLING\_MODE

FILE\_HANDLING\_MODE 설정에 따라 다음과 같은 테이블을 생성합니다.

> 첨부파일 테이블 : **BIZ\_ATTACHMENTS**
>
> * 메시지 발송을 위한 첨부파일 데이터가 입력되는 테이블

> 첨부파일 로그 테이블 : **BIZ\_ATTACHMENTS\_LOG\_YYYYMM**
>
> * 첨부파일 테이블에서 발송 결과 업데이트가 완료된 데이터가 이동되는 테이블

{% hint style="info" %}
ATTACHMENTS\_BACKUP\_OPTION(Y/N, default N)을 사용하지 않으면

첨부파일 테이블의 데이터를 재사용 할 수 있습니다.
{% endhint %}

참고 : [\[첨부파일 관리\]](../appendix.md#undefined-1)

![](<../.gitbook/assets/image (5) (1) (1).png>)
