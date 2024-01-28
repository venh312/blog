### 1. 기존 도커 제거 (선택 사항)
   이전에 이미 도커가 설치되어 있다면, 제거할 수 있습니다. 아래 명령어를 사용하여 도커를 제거합니다.
   ```bash
   sudo apt remove docker docker-engine docker.io containerd runc
   ```

### 2. 도커 설치
   도커 공식 설치 스크립트를 사용하여 도커를 설치할 수 있습니다. 다음 명령어를 사용하여 스크립트를 실행합니다.
   ```bash
   curl -fsSL https//get.docker.com -o get-docker.sh
   sudo sh get-docker.sh
   ```

   위 명령어는 curl을 사용하여 도커 설치 스크립트를 다운로드하고, 그 스크립트를 실행하여 도커를 설치합니다.

### 3. 도커 그룹에 사용자 추가 (선택 사항)
   도커 명령어를 실행할 때마다 `sudo`를 사용하지 않도록 하려면 현재 사용자를 도커 그룹에 추가할 수 있습니다.
   ```bash
   sudo usermod -aG docker $USER
   ```

   그러나 이 작업을 수행한 후에는 로그아웃하고 다시 로그인해야 변경 사항이 적용됩니다.

### 4. 도커 서비스 시작
   도커를 설치한 후에는 도커 서비스를 시작해야 합니다.
   ```bash
   sudo systemctl start docker
   ```

   부팅 시 자동으로 시작하도록 설정하려면 다음 명령어를 사용합니다.
   ```bash
   sudo systemctl enable docker
   ```

### 5. 도커 버전 확인
   도커가 정상적으로 설치되었는지 확인하려면 다음 명령어를 사용합니다.
   ```bash
   docker --version
   ```
