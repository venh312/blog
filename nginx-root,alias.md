## root
```
location /test/ {
   root /home/www/project/;
}
```
/home/www/project/test/ 의 경로에서 파일을 찾는다.

## alias
```
location /test/ {
   alias /home/www/project/;
}
```
/home/www/project/ 의 경로에서 파일을 찾는다.
/test/를 생략한다.
