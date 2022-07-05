# Agent Install

## Linux/Unix 계열

1. 비즈클라이언트를 서버에 업로드 한 뒤 압축 해제합니다. **`unzip biz_client_v3xxx.zip`**
2. 환경 설정 파일을 수정합니다. _**`{모듈경로}/config/uds.conf`**_
   1. 계정 설정 : [biz.ppurio.com](http://biz.ppurio.com) 사이트의 계정을 설정합니다. **(옵션: UDS\_ID, UDS\_PW)**
   2. DBMS 연결 정보 설정 **(옵션: DBNAME, DBURL, DBUSER, DBPASS)**
3. 비즈클라이언트를 시작합니다.\
   _**`{모듈경로}/script`**_\*\* → `./biz_start`\*\*
4. 비즈클라이언트를 중지합니다.\
   _**`{모듈경로}/script`**_\*\* → `./biz_stop`\*\*

{% embed url="https://youtu.be/kAG-_nNXty8" %}

## Windows 계열

1. 비즈클라이언트를 서버에 업로드 한 뒤 압축 해제합니다. **`unzip biz_client_v3xxx.zip`**
2. 환경 설정 파일을 수정합니다. _**`{모듈경로}/config/uds.conf`**_
   1. 계정 설정 : [biz.ppurio.com](http://biz.ppurio.com) 사이트의 계정을 설정합니다. **(옵션: UDS\_ID, UDS\_PW)**
   2. DBMS 연결 정보 설정 **(옵션: DBNAME, DBURL, DBUSER, DBPASS)**
3. 비즈클라이언트를 설치/시작합니다. _**`{모듈경로}/bat`**_\
   설치 : <mark style="color:orange;">service-install.bat 실행 (관리자권한)</mark>\
   &#x20;cf) 비즈클라이언트 등록 확인 :\
   &#x20;       제어판 → 관리도구 → 서비스 (Daoutech BizClient 서비스를 통하여 직접 시작/종료 가능)\
   시작 : service-start.bat 실행
4. 비즈클라이언트를 중지합니다. _**`{모듈경로}/bat`**_\
   중지 : <mark style="color:orange;">service-stop.bat</mark>\ <mark style="color:orange;"></mark>서비스 삭제 : <mark style="color:orange;">service-uninstall.bat</mark>

{% embed url="https://youtu.be/D_HFawjw68c" %}

{% hint style="info" %}
uds.conf 파일은 EUC-KR 로 인코딩 되어 있습니다.
{% endhint %}
