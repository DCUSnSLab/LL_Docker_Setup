# 개요

리빙랩 CMS의 메인 서버, 쉘터 서버 Deploy를 용이하게 진행하기 위한 저장소입니다.

# 이미지 별 정보

Dockerfile 참고

## snslabdocker/cms_main
Main 서버가 실행되는 image입니다.

root 경로에 [LivingLab-CCS (Main Branch)](https://github.com/DCUSnSLab/LivingLab-CCS/tree/Main)가 clone되어 있으며,

docker-compose를 통한 최초 Deploy 수행 시

Livinglab_CMS/Livinglab/Livinglab-CMS(Main)/cms_main_server/start_cms.sh

에 있는 스크립트 실행을 통해 Main 서버를 시작합니다.

데이터베이스의 경우 5432번 포트를 통해 Postgres 컨테이너를 사용하며,

8000번 포트를 통해 서비스를 제공합니다.

## snslabdocker/cms_shelter
Shelter 서버가 실행되는 image입니다.

root 경로에
- [LivingLab-ShelterServer (LP-86shelterCMS_ADD Branch)](https://github.com/DCUSnSLab/LivingLab-ShelterServer/tree/LP-86shelterCMS_ADD)
- [LivingLab-CMS-IDLE (IDLE_2 Branch)](https://github.com/DCUSnSLab/LivingLab-CMS-IDLE.git)
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
docker-compose -f docker-compose_main.yml up -d
```

# 설정

각각의 docker-compose_*.yml 파일의 HOST_IP 환경변수 옵션을 현재 장치의 ip 주소로 설정해야 합니다. (QR Code 생성 및 접근을 위함)