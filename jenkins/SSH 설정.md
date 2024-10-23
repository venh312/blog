## 젠킨스가 설치된 서버에서 원격지(애플리케이션 배포) 서버에 접근하는 `SSH` 설정 방법

### Publish Over SSH 플러그인 설치
Jenkins 관리 > Plugins

### 1. Jenkins 서버 (클라이언트)에서 설정
#### <1-1> ssh-keygen을 사용해서 RSA private key를 생성
보통 `ssh-keygen` 명령어로 생성이 되나 OPEN SSH 버전에 따라 다르게 생성되기도 한다. (OPEN SSH PRIVATE KEY 등) 이럴 경우 `ssh-keygen -t rsa -b 2048 -m PEM` 명령어로 생성한다. 

패스워드를 입력하려면 하고 생략 가능하다. 생성이 완료되면 `cd ~/.ssh` 경로에 `id_rsa`, `id_rsa.pub` 2개의 파일이 생성된다.

#### <1-2> id_rsa 파일
`id_rsa` 해당 파일의 내용은 jenkins 관리 > System -> Publish over SSH의 Key 영역에 등록 한다.

#### <1-3> id_rsa.pub 파일
```ssh-copy-id [username]@[remote_host]```
원격지 username 계정으로 공개키를 등록한다.

#### <1-3-1> 수동으로 등록하는 방법
원격지 서버에서 `cd ~/.ssh` 경로로 가서 authorized_keys 파일에 id_rsa.pub 내용을 넣는다. 여러 개 있을 경우 줄 바꿈으로 구분해서 넣는다. (이어지지 않게)

### <1-4> SSH Servers 설정
- Name : 해당 SSH를 구분 할 이름
- Hostname : 호스트 주소 (IP)
- Username : 위에서 생성한 키를 등록한 계정 (Ex. root)
- Remote Directory : 기본으로 설정할 원격지 경로 보통 `/home` 으로 설정한다.

설정이 끝나면 `Test Configuratio`n 으로 접근이 잘 되는지 확인한다.

### FreeStyle(Item) 설정
#### Item에서 git 설정 및 배포를 위한 maven, gralde 빌드 커맨드를 **Build Steps**의 shell에 커맨드를 작성한다.
#### 환경 설정에서 ssh에 rsa 키 내용 및 원격지 정보를 입력한다.
#### 원격지에 빌드된 파일이나 war 전송을 위해서는 **빌드 후 조치**에서 Send build artifacts over SSH를 작성한다.
- Source files: jenkins 설치경로/workspace/Item명을 디폴트로 바라본다.
- Remove prefix: Source files에 입력된 경로의 prefix를 삭제해준다.
- Remote directory: 원격지 서버의 경로를 지정한다. 입력하지 않을경우 Publish over SSH에 입력된 디폴트 경로를 따라간다.
- Exec command: 전송 완료 후 사용할 커맨드를 작성할 수 있다.
