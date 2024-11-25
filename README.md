
## 설치 및 환경설정

### 디렉토리 구조

### 시스템 환경 설정
### 프로젝트 생성 및 환경 설정

## REXSYS API 개발 가이드 및 명세.

### 1. 클라이언트

1.1. [클라이언트 인증 및 토큰 발급](https://github.com/digimixnet2/rexsys.docs/blob/main/api/api.client.certificate.md)

1.2. [클라이언트를 위한 Socket.IO](https://github.com/digimixnet2/rexsys.docs/blob/main/api/api.client.socketio.md)

### 2. 사용자

2.1. [사용자 체크인](https://github.com/digimixnet2/rexsys.docs/blob/main/api/api.user_event_checkin.md)

2.2. [사용자키 인증](https://github.com/digimixnet2/rexsys.docs/blob/main/api/api.user_event_certificate.md)

2.3. [사용자 로드맵](https://github.com/digimixnet2/rexsys.docs/blob/main/api/api.user_event_roadmap.md)


### 3. 미디어

3.1. [미디어 업로드](https://github.com/digimixnet2/rexsys.docs/blob/main/api/api.media.upload.md)

3.2. [미디어 목록 조회](https://github.com/digimixnet2/rexsys.docs/blob/main/api/api.media.list.md)

3.3. [좋아요 - 인기투표](https://github.com/digimixnet2/rexsys.docs/blob/main/api/api.media.like.md)

### 4. QRCODE

4.1. [QRCODE 생성 - 일반형](https://github.com/digimixnet2/rexsys.docs/blob/main/api/api.qrcode.maker.noraml.md)


### 5. 결제시스템

5.1  [아키텍처 캐시 데이터 : 기부처 목록 가져오기](https://github.com/digimixnet2/rexsys.docs/blob/main/api/api.architecture.cache.md)

5.2. [결제 내역 전송](https://github.com/digimixnet2/rexsys.docs/blob/main/api/api.payment.process.md)

5.3. [기부 통계](https://github.com/digimixnet2/rexsys.docs/blob/main/api/api.payment.statistics.md)


### 6. SNS

5.1. SNS 전송 목록 (비공개)

5.2. SNS 전송
  
### 6. 단축 URL

### 7. QR 가이드

### 8. 게시판

8.1. [글목록] (https://github.com/digimixnet2/rexsys.docs/blob/main/api/api.note_board_list.md)
8.2. [글쓰기(이미지 첨부 가능)] (https://github.com/digimixnet2/rexsys.docs/blob/main/api/api.note_board_add.md)

### *** Release Note & Issue.

#### version 2.0

2024.07.04 아키텍처 기부처 불러오기

2024.06.25 전송 파라미터의 Encode 스크립트 오류 수정.

2024.06.25 미디어 목록에서 콤마 단위의 String을 Array로 출력되게 변경( 산, 바다, 하늘 => [ "산", "바다", "하늘" ] )

2024.06.25 미디어 업로드, 노트 항목(id, name, link, content ... ) 설명 추가



