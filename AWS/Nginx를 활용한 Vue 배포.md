# Nginx를 활용한 Vue 배포

## Nginx 설치
```
sudo apt update
sudo apt upgrade
sudo apt-get install nginx
```

## Nginx Config 파일 설정
```
vi /etc/nginx/sites-available/default
```

![]()

## Nginx 재시작
```
sudo nginx -t
sudo systemctl restart nginx
```
