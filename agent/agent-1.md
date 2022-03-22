# Agent 설정

**uds.conf**

```python
DBURL = jdbc:mysql://<DB 호스트 IP>:<DB 호스트 PORT>/<DB 이>?useUnicode=true&
        characterEncoding=euc-kr&useSSL=false&allowPublicKeyRetrieval=true
```

> 클라이언트 실행 후에는 uds.confx 로 파일명이 변경됨
>
> * 비즈뿌리오 비밀번호나 DB 비밀번호를 수정해야 할 때 .confx -> .conf로 변경한 뒤 수정
> * 암호화 된 비밀번호 삭제 후 재작성

