## apt update 
설치 가능한 패키지 리스트를 최신화

## net-tools, vim, openssh-server, ufw 를 설치
```apt install net-tools vim openssh-server ufw```

## ssh 접근 허용
```ufw allow ssh```

## sshd_config 수정
root 계정으로 연결 할 것이기 때문에 /etc/ssh/sshd_config 파일을 수정한다.

```vi /etc/ssh/sshd_config```
상기 명령을 통해 진입 후, PermitRootLogin 부분을 yes 로 변경한다. (주석 해제 및 yes 로 변경)

## root 계정 비밀번호 설정
sudo passwd root 

service ssh start 혹은 이미 ssh 를 시작한 경우라면 service ssh restart 를 통해 ssh 를 시작한다.
```service ssh start```
```service ssh restart```
