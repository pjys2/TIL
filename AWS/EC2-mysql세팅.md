## EC2(Ubuntu)에 mysql세팅하기

## Mysql 설치
ssh를 통해 EC2 인스턴스에 접속해서 다음 명령어를 입력한다.
```
sudo apt-get update
```
```
sudo apt-get install mysql-server
```

## Mysql 접속
* 다음 명령어를 통해 mysql에 접속한다.
* 최초 패스워드가 설정되어 있지 않기 때문에 엔터를 치면 바로 로그인이 가능하다.
```
sudo mysql -u root -p
```

