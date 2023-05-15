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

## 인원 별 저장소 및 개발 내용

Jira의 각 티켓 참고해서 아래 저장소 기반 작업 진행하면 될 것 같습니다.

Main을 제외한 Shelter 파트 작업 진행자들의 경우

https://github.com/DCUSnSLab/LL_Shelter_Sinage

해당 저장소의 README를 참고하여 로컬에 환경 구축 후 진행하면 됩니다.

- Main
  - Contents upload UI (노동원, 환경구축 과정이 위와 다르므로 별도 진행)
    - 저장소 및 작업 경로
      - https://github.com/DCUSnSLab/LL_Main
      - https://github.com/DCUSnSLab/LL_Main/tree/Main/Livinglab_CMS/Livinglab/Livinglab-CMS/cms_main_server/templates/Userservice
    - 업로드 페이지 URL
      - http://203.250.35.123:8000/Userservice/UploadContent/1 
      - http://203.250.35.123:8000/Userservice/AddCommunityComment/1


- Shelter
  - Client
    - Sinage IDLE 페이지 (박보은)
      - 저장소 및 작업 경로
        - https://github.com/DCUSnSLab/LL_Shelter_Sinage
        - https://github.com/DCUSnSLab/LL_Shelter_Sinage/tree/IDLE_2/Client/client_react/src/component
    - Sinage Contents 리스트 페이지 (김경연)
      - 저장소 및 작업 경로
        - https://github.com/DCUSnSLab/LL_Shelter_Sinage
        - https://github.com/DCUSnSLab/LL_Shelter_Sinage/blob/IDLE_2/Client/client_react/src/component/SignageShow.js
    - MediaPlayer (문지원)
    - Community (임찬아)
      - 저장소 및 작업 경로
        - https://github.com/DCUSnSLab/LL_Shelter_Sinage
        - https://github.com/DCUSnSLab/LL_Shelter_Sinage/blob/IDLE_2/Client/client_react/src/component/IssueBoard.js
  - Server
    - API-Server (박준홍)