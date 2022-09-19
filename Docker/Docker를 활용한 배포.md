# Docker를 활용한 배포

## Docker 설치 방법
### 저장소 설정
1. Update the apt package index and install packages to allow apt to use a repository over HTTPS:
```
sudo apt-get update
```
```
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

2. Add Docker’s official GPG key:
```
sudo mkdir -p /etc/apt/keyrings
```
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

3. Use the following command to set up the repository:
```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### 도커 엔진 설치
```
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

### 도커 테스트
```
sudo docker pull hello-world
```
![pull hello-world]()
```
sudo docker run hello-world
```
![run hello-world]()

* 도커 작동 상태 확인
```
sudo docker ps -a
```
* 도커 테스트



[우분투 도커 설치 공식문서](https://docs.docker.com/engine/install/ubuntu/)
