## Memory
### 보통 free -h를 많이 사용

#### 메모리 사용량 확인
```free```

#### KB 단위로 확인 [-b | -k | -m | -g]
```free -k```

#### MB 단위로 확인 [-b | -k | -m | -g]
```free -m```

#### 사람이 읽기 쉬운 단위로 확인
```free -h```

#### 와이드 모드로 cache와 buffers를 따로 출력
```free -w ```

## CPU
#### CPU 확인
```cat /proc/cpuinfo```

#### CPU 전체 코어 개수
```grep -c processor /proc/cpuinfo```

#### 물리적 CPU 개수
```grep "physical id" /proc/cpuinfo | sort -u```

#### CPU 물리적 코어 개수
```grep "cpu cores" /proc/cpuinfo | tail -1```

## Disk
### 보통 df -h를 많이 사용

#### 남은 용량 확인
```df```
#### KB 단위로 확인
```df -k```
#### MB 단위로 확인
```df -m```
#### 사람이 읽기 쉬운 단위로 확인
```df -h```
