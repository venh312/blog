## 원격지의 암호 물어보지 않게 하는 방법
sshpass를 이용하여 명령어에 암호를 같이 입력하여 명령어 입력으로만 ssh 명령어 사용 가능

## sshpass 설치 방법
```sudo apt-get install sshpass```
 
### ssh 접속
```sshpass -p [원격지 접속 계정의 암호] ssh root@192.168.0.1```   

### 원격지에 있는 루트 경로에 있는 test.sh 실행
```sshpass -p [원격지 접속 계정의 암호] ssh root@192.168.0.1 "sh /test.sh" ```   

### scp를 이용한 파일 전송 -test.txt 파일을 원격지 /home 경로에 전송
```sshpass -p [원격지 접속 계정의 암호] scp test.txt root@192.168.0.1:/home```
 
### sshpass 사용 방법
```ubuntu@ubuntu-VirtualBox:~$ sshpass -h```   
```Usage: sshpass [-f|-d|-p|-e] [-hV] command parameters
   -f filename   Take password to use from file
   -d number     Use number as file descriptor for getting password
   -p password   Provide password as argument (security unwise)
   -e            Password is passed as env-var "SSHPASS"
   With no parameters - password will be taken from stdin

   -P prompt     Which string should sshpass search for to detect a password prompt
   -v            Be verbose about what you're doing
   -h            Show help (this screen)
   -V            Print version information
At most one of -f, -d, -p or -e should be used```
