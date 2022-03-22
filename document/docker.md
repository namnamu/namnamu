# 도커

git clone한 파일 내에서

docker run -it node를 실행 시, 내 컴퓨터에 있는 노드 우선 실행하고, 없으면 이미지 다운받아서 컨테이너로 해동함.

> $ docker images                                             로컬 컴퓨터에 저장하고 있는 이미지 리스트를 보는 명령

> $ docker ps                                                     컨테이너 확인명령

$ docker exe -it 컨테이너명 bash                   실행되어 있는 컨테이너 내부 구조를 확인할 수 있다.

 docker ps로 컨테이너가 철거된것은 나타나지 않음

docker ps -a로 중단된 것들도 다 보이도록함.

[https://rayner.tistory.com/31](https://rayner.tistory.com/31)

docker pull ubuntu:18.04           이미지를 다운로드하는 예시

   ---
### Image를 이용해서 Container 인스턴스를 만드는 역할

> **docker create [옵션] 이미지 이름[:버전]** 
>
> docker create -i -t --name webserver centos:8

방금 만든 도커 컨테이너를 실행하는 명령은 docker start입니다. 추가로 컨테이너를 실행한 후 컨테이너 내로 진입하는 명령은 docker attach입니다.

> docker start 컨테이너 이름
>
> **docker attach 컨테이너 이름**
   
---
### 컨테이너 중지

> docker stop <container name>
   
   ---
### git 설치

[https://jjeongil.tistory.com/1304](https://jjeongil.tistory.com/1304)

> apt update
>
> apt install git
>
> git --version


**apt-get install unzip**
