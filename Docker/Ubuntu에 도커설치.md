## Ubuntu에 도커설치

### 저장소 설정
1. HTTPS를 통해 리포지토리를 사용할 수 있도록 패키지 인덱스를 업데이트하고 apt패키지를 설치한다.
``` ubuntu
 $ sudo apt-get update
 
 $ sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```
2. Docker의 공식 GPG키 추가:
```
$ sudo mkdir -p /etc/apt/keyrings
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
