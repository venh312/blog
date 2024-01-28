## 해당 패키지 내용은 모두 `Ubuntu 22.04 LTS` 기준으로 작성되었습니다.

### 운영체제 확인
```bash
lsb_release -a
```

### 디스크 사용량 확인
```bash
df -h  
```

### 메모리 사용량 확인
```bash
free -h
```

### 온도 확인
#### lm-sensors 패키지 설치
```bash
sudo apt-get install lm-sensors
```

#### 설치 후에는 `sensors` 명령어로 온도를 확인할 수 있습니다.
```bash
sensors
```
