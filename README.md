# 개요

리빙랩 CMS의 메인 서버, 쉘터 서버 Deploy를 용이하게 진행하기 위한 저장소입니다.

# 설치

해당 저장소 clone 후 docker-compose.yml 파일이 있는 경로에서 아래 명령어 수행

```docker-compose -f docker-compose.yml up -d```

### TODO List
- 최초 실행 시 필요한 일부 과정 자동화
  - [X] docker-compose 후 db migration 자동화
  - [ ] Django 관리자 계정 생성
  - [ ] FTP 동기화 서버 실행
- [ ] 기능 동작 테스트