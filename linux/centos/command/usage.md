## Memory


## CPU
### 1. CPU 확인
```cat /proc/cpuinfo```

### 2. CPU 전체 코어 개수
```grep -c processor /proc/cpuinfo```

### 3. 물리적 CPU 개수
```grep "physical id" /proc/cpuinfo | sort -u```

### 4. CPU 물리적 코어 개수
```grep "cpu cores" /proc/cpuinfo | tail -1```

## Disk
