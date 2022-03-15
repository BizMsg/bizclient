---
description: 비즈클라이언트란?
---

# 개요 및 선결 조건

### 개요

고객사 시스템 환경에 설치하여 비즈뿌리오 서비스와 연동하는 모듈로,\
이동통신사 기반의 메시지(SMS/LMS/MMS), RCS, 카카오톡 비즈메시지 (AT/FT/BI/BW), PHONE, FAX를 \
발송할 수 있게 연계합니다.

### 선결 조건

1. 서비스 계정 생성\
   biz.ppurio.com 회원가입
2. 서비스 사용 승인요청\
   문의전화 : 1599-9782\
   E-mail : bizppurio@daou.co.kr
3. 카카오톡 비즈메시지 사용
   1. 카카오톡 채널 개설 및 비카카오톡 채널 개설 및 비즈니스 채널 신청 (https://center-pf.kakao.com)
   2. 발신프로필키 생성 (비즈뿌리오 사이트에서 사용자가 직접 진행)
   3. 알림톡의 경우, 템플릿 승인 필요 (비즈뿌리오 사이트에서 사용자가 직접 진행)
   4. 친구톡에 이미지를 삽입하는 경우, 이미지 등록 필요 (비즈뿌리오 사이트에서 사용자가 직접 진행)
4. RCS 사용
   1. RCS 브랜드 개설 및 대행사 설정 (https://www.rcsbizcenter.com)
   2. RCS 브랜드 등록 (비즈뿌리오 사이트에서 사용자가 직접 진행)
   3. RCS 발신번호 등록 (비즈뿌리오 사이트에서 사용자가 직접 진행)
   4. RCS 템플릿의 경우, 템플릿 승인 필요 (비즈뿌리오 사이트에서 사용자가 직접 진행)



### 연동 방식

비즈클라이언트는 고객사의 데이터베이스 연동을 통하여 메시지를 발송하는 모듈입니다. \
고객사의 데이터베이스에 테이블을 생성한 후 발송에 필요한 데이터를 입력하면, 비즈클라이언트는 이를 체크하여 \
메시지를 발송하는 방식입니다.
