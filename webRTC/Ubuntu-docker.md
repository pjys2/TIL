# Ubuntu에 Docker 설치하기

이 글은 윈도우 운영체제에서 우분투를 설치해서 도커를 설치하는 방법을 다룬다.

## Ubuntu설치하기
![우분투 설치](https://github.com/JaeyeongPark/TIL/blob/main/webRTC/img/%EC%9A%B0%EB%B6%84%ED%88%AC%EC%84%A4%EC%B9%98.PNG)
* Microsoft Store에서 우분투를 설치한다.

## Docker 설치
* 설치한 우분투를 실행시킨다.

[우분투 도커 설치 공식문서 참고](https://docs.docker.com/engine/install/ubuntu/)
[우분투 도커 설치 참고 블로그](https://teang1995.tistory.com/19)

### 저장소 설정
1. HTTPS를 통해 레포지토리를 사용할 수 있도록 인덱스를 업데이트하고 apt패키지를 설치한다.
```
$ sudo apt-get update

$ sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

2. Docker의 공식 GPG 키 추가 :
```
$ sudo mkdir -p /etc/apt/keyrings
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

3. 다음 명령을 사용하여 레포지토리 설정
```
$ echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null 
```

### 도커 엔진 설치
1. apt패키지 인덱스를 업데이트하고 최신 버전 의 Docker Engine, containerd 및 Docker Compose를 설치하거나 다음 단계로 이동하여 특정 버전을 설치합니다.
```
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

* 다음과 같은 문제 발생 시 [참고](https://boying-blog.tistory.com/82)
* ![도커엔진설치에러](https://github.com/JaeyeongPark/TIL/blob/main/webRTC/img/%EB%8F%84%EC%BB%A4%EC%97%94%EC%A7%84%20%EC%84%A4%EC%B9%98%EC%97%90%EB%9F%AC.PNG)



2. 특정 버전 의 Docker Engine 을 설치하려면 리포지토리에 사용 가능한 버전을 나열한 다음 다음을 선택하여 설치합니다.
```
$ apt-cache madison docker-ce
```
```
$ sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io docker-compose-plugin
```

3. hello-world 이미지 를 실행하여 Docker 엔진이 올바르게 설치되었는지 확인하십시오 .

```
$ sudo docker run hello-world
```

* 다음과 같은 문제 발생 시 [참고](https://velog.io/@pop8682/Docker-Cannot-connect-to-the-Docker-daemon-at-unixvarrundocker.sock.-Is-the-docker-daemon-running-%EC%97%90%EB%9F%AC-%ED%95%B4%EA%B2%B0)
* ![docker-ce 설치에러](https://github.com/JaeyeongPark/TIL/blob/main/webRTC/img/docker-ce%EC%84%A4%EC%B9%98%EC%97%90%EB%9F%AC.PNG)

