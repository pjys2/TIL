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
![mysql로그인](https://github.com/JaeyeongPark/TIL/blob/main/AWS/Mysql/img/sudo%20mysql.PNG)

## Mysql 패스워드 변경
1. 먼저 user테이블의 plugin을 확인한다.
```SQL
SELECT user, host, plugin FROM mysql.user;
```
![plugin확인](https://github.com/JaeyeongPark/TIL/blob/main/AWS/Mysql/img/mysql%20user%ED%85%8C%EC%9D%B4%EB%B8%94.PNG)\
* root의 플러그인이 auth_socket으로 되어있는데 이 부분을 caching_sha2_password로 바꿔야 패스워드를 변경할 수 있다.

2. plugin변경
```sql
UPDATE mysql.user SET plugin='caching_sha2_password' WHERE user='root';
FLUSH PRIVILEGES;
```
![plugin 변경](https://github.com/JaeyeongPark/TIL/blob/main/AWS/Mysql/img/plugin%EB%B3%80%EA%B2%BD.PNG)

3. 패스워드 변경
```sql
ALTER USER 'user'@'localhost' IDENTIFIED BY '변경할 패스워드'
SELECT user,host,authentication_string FROM user;
```
![변경한 패스워드](https://github.com/JaeyeongPark/TIL/blob/main/AWS/Mysql/img/root%ED%8C%A8%EC%8A%A4%EC%9B%8C%EB%93%9C%20%EC%83%81%ED%83%9C.PNG)



## Mysql워크벤치에 EC2 Mysql 연결하기 
* Mysql 워크벤치
![Mysql 워크벤치](https://github.com/JaeyeongPark/TIL/blob/main/AWS/Mysql/img/%EC%9B%8C%ED%81%AC%EB%B2%A4%EC%B9%98.PNG)
* Public IP를 입력하고 접속할 계정과 패스워드를 입력하고 ok를 누른다.
![Mysql 연결](https://github.com/JaeyeongPark/TIL/blob/main/AWS/Mysql/img/%EC%9B%8C%ED%81%AC%EB%B2%A4%EC%B9%98%20%EC%97%B0%EA%B2%B0.PNG)

* EC2 Public IP 찾는 명령어
```
sudo curl ifconfig.me
```
