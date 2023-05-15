# 리빙랩 개발 환경 구성

## 필요 소프트웨어

- Docker
- Docker-compose

## CMS를 통한 Main 서버 쉘터 생성

아래 주소를 통해 Main 서버에 접속한다.

[Main Server](http://203.250.35.123:8000/Login/)

이후 아래 계정으로 로그인을 진행한다.

- id
  - admin
- pw
  - 20121208

![img.png](README_img/img_1.png)

대시보드 왼쪽 메뉴에서 ```쉘터``` 메뉴를 클릭한다.

![img.png](README_img/img_2.png)

이후 ```쉘터 등록``` 버튼을 클릭하여 새 쉘터를 생성한다.

![img.png](README_img/img_3.png)

임의의 쉘터명, 소개, 주소, 프로필 이미지 파일 입력 후 등록 버튼을 클릭한다.

## docker-compose 내용 수정 및 빌드

![img.png](README_img/img_4.png)

생성된 쉘터의 번호, 쉘터명, 인증번호를

docker-compose_shelter.yml 파일의 아래 항목에 입력한다.

![img.png](README_img/img_5.png)

docker-compose_shelter.yml 파일이 있는 경로에서 아래 명령어를 통해 compose를 수행한다.

```bash
docker-compose -f docker-compose_shelter.yml up -d
```

## 파트 별 환경 구축 및 개발 수행

- Main
  - Contents upload UI (노동원, 임찬아)


- Shelter
  - Client
    - Sinage (박보은)
    - MediaPlayer (문지원)
  - Server
    - API-Server (박준홍)