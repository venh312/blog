### 아래 순서에 따라 Java 17를 설치합니다.

### 1. Java 설치 확인
   먼저 시스템에 Java가 설치되어 있는지 확인합니다.

   ```bash
   java -version
   ```

   이 명령을 실행하여 설치된 Java 버전을 확인할 수 있습니다.

### 2. Java 설치
   만약 Java가 설치되어 있지 않다면, 다음 명령으로 OpenJDK를 설치합니다.

   ```bash
   sudo apt update
   sudo apt install openjdk-17-jdk
   ```

   원하는 Java 버전에 따라 패키지 이름을 변경할 수 있습니다.

### 3. Java Home 경로 확인
   Java가 정상적으로 설치되면, Java Home 디렉토리 경로를 확인합니다. 일반적으로는 `/usr/lib/jvm/java-17-openjdk-amd64/`와 같은 경로일 것입니다.

### 4. 환경변수 설정
   다음으로, JAVA_HOME 환경변수를 설정합니다. 환경변수는 주로 `~/.bashrc` 파일에 추가하여 로그인할 때마다 자동으로 로드되도록 설정합니다. 아래 명령어로 편집기를 엽니다.

   ```bash
   nano ~/.bashrc
   ```

   파일의 맨 아래에 다음 라인을 추가합니다. 여기서 `/usr/lib/jvm/java-11-openjdk-amd64/`는 실제로 확인한 Java Home 경로로 바꿉니다.

   ```bash
   export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64/
   export PATH=$PATH$JAVA_HOME/bin
   ```

   수정을 저장하고 나온 후에는 다음 명령을 실행하여 변경사항을 적용합니다.

   ```bash
   source ~/.bashrc
   ```

### 5. 설정 확인
   환경변수가 올바르게 설정되었는지 확인합니다.

   ```bash
   echo $JAVA_HOME
   ```

   이 명령은 JAVA_HOME 환경변수의 값을 출력합니다. 값이 올바르게 설정되었다면 Java Home 경로가 출력됩니다.

---

### ❓ 설치한 java를 삭제하고 싶으면 "apt remove" 명령어를 사용한다.
`sudo apt remove openjdk-17-jdk`
