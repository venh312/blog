IDE에서는 Run > Run configurations에서 profile 설정을 할 수 있다.

하지만 war 패키징해서 별도의 서버에 톰캣을 이용해서 배포해야 할 경우 설정이 따로 필요하다.

**방법은 톰캣 설치 경로에 있는 bin 폴더에 setenv.sh 파일을 생성해서 아래 명령어를 입력한다.**

### vi 또는 vim
```vi setenv.sh```

### 아래 내용 입력 (해당 톰캣에 설정할 profile 지정 dev,prod 등등)
```
export JAVA_OPTS="-Dspring.profiles.active=dev"
```

### 저장
입력 후 순서대로 ```esc 키 > :  > wq!```

### 파일 권한 변경
```chmod -777 setenv.sh```

startup.sh 호출 > catalina.sh 호출 > setenv.sh 파일 있으면 참조
