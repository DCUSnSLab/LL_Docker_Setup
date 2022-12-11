# 개요

리빙랩 CMS의 메인 서버, 쉘터 서버 Deploy를 용이하게 진행하기 위한 저장소입니다.

# Docker image

## snslabdocker/cms_main
Main 서버가 실행되는 image입니다.

root 경로에 [LivingLab-CCS (Main Branch)](https://github.com/DCUSnSLab/LivingLab-CCS/tree/Main)가 clone되어 있으며,

docker-compose를 통한 최초 Deploy 진행 시

Livinglab_CMS/Livinglab/Livinglab-CMS(Main)/cms_main_server/start_cms.sh

에 있는 스크립트 실행을 통해 Main 서버를 시작합니다.

## snslabdocker/cms_shelter
Shelter 서버가 실행되는 image입니다.



# 설치

해당 저장소 clone 후 아래 명령어 수행

하나의 Host에 Main, Shelter 둘 다 구축하는 경우

```docker-compose -f docker-compose.yml up -d```

CMS Main 서버만 구축하는 경우

```docker-compose -f docker-compose_main.yml up -d```

CMS Shelter 서버만 구축하는 경우

```docker-compose -f docker-compose_main.yml up -d```

### TODO List
- 최초 실행 시 필요한 일부 과정 자동화
  - [X] docker-compose 후 db migration 자동화
  - [X] Django 관리자 계정 생성
  - [ ] FTP 동기화 서버 실행
- [ ] 기능 동작 테스트
