# 개요

리빙랩 CMS의 메인 서버, 쉘터 서버 Deploy를 용이하게 진행하기 위한 저장소입니다.

# 이미지 별 정보

## snslabdocker/cms_main

### 환경 구성

- Ubuntu 22.04
- Python 3.10.6
- Django 4.1.7

### 내용

Main 서버가 실행되는 image입니다.

root 경로에 [LivingLab-CCS (Main Branch)](https://github.com/DCUSnSLab/LivingLab-CCS/tree/Main)가 clone되어 있으며,

docker-compose를 통한 최초 Deploy 수행 시

Livinglab_CMS/Livinglab/Livinglab-CMS(Main)/cms_main_server/start_cms.sh

에 있는 스크립트 실행을 통해 Main 서버를 시작합니다.

데이터베이스의 경우 5432번 포트를 통해 Postgres 컨테이너를 사용하며,

8000번 포트를 통해 서비스를 제공합니다.

## snslabdocker/cms_shelter

### 버전 종속성
- Ubuntu 22.04
- Python 3.10.6
- NVM(NPM) 8.15.0
- Django 4.2

### 저장소 구성 및 역할
- [LivingLab-ShelterServer (LP-86shelterCMS_ADD Branch)](https://github.com/DCUSnSLab/LivingLab-ShelterServer/tree/LP-86shelterCMS_ADD)
  - 최초 Deploy 시 Django 기반 데이터베이스 구축
  - API 서버 역할 수행
  - CMS-IDLE의 Client/client-react/public/ftp 경로와 심볼링 링크로 연결되어 있습니다. (API 서버에서 이미지 및 영상 기반 쿼리 수행 시 데이터 전송 위함)
- [LivingLab-CMS-IDLE (IDLE_2 Branch)](https://github.com/DCUSnSLab/LivingLab-CMS-IDLE.git)
  - React 기반 프론트엔드 역할 수행
  - 광고 페이지, 컨텐츠, 커뮤니티 페이지 출력
  - 컨테이너 최초 시작 시 start_shelter.sh 스크립트 실행
  - Server/ 경로의 advertiser.py 스크립트를 통해 Django 데이터베이스에서 조회한 쿼리 결과를 Websocket 형태로 전송
  - ftpMediaDownloadClient.py 파일을 통한 Main - Shelter 간 데이터 
- [Livinglab_WiFi](https://github.com/DCUSnSLab/Livinglab_WiFi)
  - 와이파이 페이지 출력을 위한 저장소

Shelter 서버가 실행되는 image입니다.

root 경로에
- [LivingLab-ShelterServer (LP-86shelterCMS_ADD Branch)](https://github.com/DCUSnSLab/LivingLab-ShelterServer/tree/LP-86shelterCMS_ADD)
- [LivingLab-CMS-IDLE (IDLE_2 Branch)](https://github.com/DCUSnSLab/LivingLab-CMS-IDLE.git)
- [Livinglab_WiFi](https://github.com/DCUSnSLab/Livinglab_WiFi)
가 clone되어 있으며,

docker-compose를 통한 최초 Deploy 수행 시

/root/LivingLab-CMS-IDLE/start_shelter.sh

에 있는 스크립트 실행을 통해 Shelter 서버를 시작합니다.

데이터베이스의 경우 5433번 포트를 통해 Postgres 컨테이너를 사용하며,
(동일 Host에서 Main 서버와 병렬 구성 시 발생하는 충돌 방지 위함)

8000번 포트를 통해 서비스를 제공합니다.

# 설치

해당 저장소 clone 후 아래 명령어 수행

하나의 Host에 Main, Shelter 둘 다 구축하는 경우

```
docker-compose -f docker-compose.yml up -d
```

CMS Main 서버만 구축하는 경우

```
docker-compose -f docker-compose_main.yml up -d
```

CMS Shelter 서버만 구축하는 경우

```
docker-compose -f docker-compose_shelter.yml up -d
```

각각의 .yml 파일 내에 있는 환경 변수를 설정해야 합니다.
(docker-compose_shelter.yml 내용 참고)

메인 및 쉘터 컨테이너의 이미지가 최신 태그인지 아래 링크에서 확인 후 버전 변경 후 진행하도록 합니다.

[cms_main](https://hub.docker.com/r/snslabdocker/cms_main)

[cms_shelter](https://hub.docker.com/r/snslabdocker/cms_shelter/tags)

# 초기 구성

## Main

localhost:8000/admin 경로로 이동 후 아래 admin 계정으로 로그인

- id : admin
- pw : 20121208

이후 사이트 관리 아래 메뉴의 Custom users를 추가한다.

User auth 및 User status는 각각 Super_Admin, ACTIVATE 로 설정한다.

localhost:8000/ 로 이동한 다음, 메인 메뉴의 계정인증 버튼을 누르고 아래 admin 계정으로 로그인한다.

- id : admin
- pw : 20121208

이후 해당 페이지에서 쉘터 등록 및 컨텐츠 업로드를 수행한다.

## Shelter

각각의 docker-compose_*.yml 파일의 HOST_IP 환경변수 옵션을 현재 장치의 ip 주소로 설정해야 합니다. (QR Code 생성 및 접근을 위함)
