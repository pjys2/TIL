# Nginx에 https세팅하기

## Nginx SSL적용 및 SpringBoot proxy설정
* letsencrypt 설치하기
```
sudo apt-get update -y & sudo apt-get install letsencrypt -y
```
* nginx 중지
```
sudo service nginx stop
```
* 인증서 발급
```
sudo letsencrypt certonly --standalone -d [도메인 네임]
```
![SSL키발급]()

* conf파일 설정
```
vi /etc/nginx/sites-availables/default
```

![nginx설정]()


* nginx 재가동
```
sudo service nginx restart
```
