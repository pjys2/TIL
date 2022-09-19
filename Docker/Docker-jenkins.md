# 젠킨스 설치(도커 컨테이너)
* docker-compose.yml생성
```
vim docker-compose.yml
```

* docker-compose.yml파일 내용
```
version: '3'

services:
    jenkins:
        image: jenkins/jenkins:lts
        container_name: jenkins
        volumes:
            - /var/run/docker.sock:/var/run/docker.sock
            - /jenkins:/var/jenkins_home
        ports:
            - "9090:8080"
        privileged: true
        user: root
```

* services : 컨테이너 서비스
* jenkins : 서비스 이름
* image : 컨테이너 생성시 사용할 image, 여기서는 jenkins/jenkins:lts 이미지를 사용(jenkins의 lts버전을 가져온다는 뜻)
* container_name : 컨테이너 이름
* volumes : 공유 폴더 느낌, aws의 /var/run/docker.sock와 컨테이너 내부의 /var/* run/docker.sock를 연결, /jenkins 폴더와 /var/jenkins_home 폴더를 연결.
* ports : 포트 매핑, aws의 9090 포트와 컨테이너의 8080 포트를 연결한다.
* privileged : 컨테이너 시스템의 주요 자원에 연결할 수 있게 하는 것 기본적으로 False로 한다고 한다.
* user : 젠킨스에 접속할 유저 계정 (root로 할 경우 관리자)

* docker-compose 실행
```
sudo docker-compose up -d
```
![]

* (에러 발생 시)If it's at a non-standard location, specify the URL with the DOCKER_HOST environment variable.
```
sudo service docker start
```

## 젠킨스 접속 (공인IP:9090)

* Administrator password 찾기
```
sudo docker logs jenkins
```

## 플러그인 설치
* GitLab플러그인
* Docker플러그인
* SSH플러그인




[참고자료](https://github.com/hjs101/CICD_manual#docker-%EC%84%A4%EC%B9%98)


