## 개요
스프링부트 war 프로젝트를 bootwar, war로 빌드하여 내장·외장 톰캣으로 실행

### 성능
내장·외장 성능에 대해서 유의미한 큰 차이는 없다고 한다. 하지만 외장 톰캣에서 virtual host 같은 기능의 구성 시 간단하게 적용 가능하다.

### virtual host
도메인 host에 따라 각각의 다른 루트 컨텍스트를 갖게하여 하나의 웹 애플리케이션 배포만으로 마치 여러 애플리케이션을 운영하는것처럼 하는 기능

### bootWar
내장 톰캣 실행 가능, 외장 톰캣 실행 가능

### war
내장 톰캣 실행 불가, 외장 톰캣 실행 가능

### 패키지 구성의 차이
|bootWar|war|
|---|-------|
|WEB-INF|WEB-INF|
|META-INF|META-INF|
|org||

- **bootWar**의 경우, 내장 톰캣으로 단독 실행이 가능 하게 하는 **WEB-INF > lib-provided** 구성이 존재한다.

## 배포 실습

### 구성 환경
Java 1.8, Spring Boot 2.7.8, Gradle, IntelliJ Community

### 프로젝트 환경 - [Spring initializr](https://start.spring.io/)
![1](https://user-images.githubusercontent.com/13326651/219359023-49d286aa-58bb-4fcc-b51b-3e5998617e2d.PNG)

### 테스트 컨트롤러 생성
![image](https://user-images.githubusercontent.com/13326651/219362921-90b60fff-2191-4c8f-a077-0fb0ad37e223.png)   
호출 테스트를 위해 @RestContoller로 간단한 테스트 컨트롤러를 생성한다.

## bootWar 빌드
2가지 방법으로 빌드 할 수 있다. **IDE** 를 통해 하는 방법과 **gradlew** 으로 빌드하는 방법을 소개한다.

### IntelliJ
![image](https://user-images.githubusercontent.com/13326651/219365981-1118c935-20d9-4037-a4be-37db2bdaad1d.png)

### gradlew
프로젝트 경로로 이동, 아래 명령어 입력   
```./gradlew bootWar```

## bootWar 구조 (/프로젝트/build/libs)
![image](https://user-images.githubusercontent.com/13326651/219383955-0c0263bf-2772-42e5-8291-0a98569bcd00.png)

## 내장 톰캣 실행
프로젝트 경로로 이동, 아래 명령어 입력   
```java -jar toy-0.0.1-SNAPSHOT.war```   

![image](https://user-images.githubusercontent.com/13326651/219386974-b44b9fb8-8ec8-45b0-b9ad-e92af30c92e8.png)

## 외장 톰캣 실행

### 톰캣 설치 - [Download](https://tomcat.apache.org/download-90.cgi)
![2](https://user-images.githubusercontent.com/13326651/219393787-df7a45c3-a89e-4c75-af9b-c61d39e58d87.PNG)   
사용중인 운영체제에 맞게 톰캣을 다운로드 받는다.

### war 파일 > 외장 톰캣 webapps 경로로 이동
![image](https://user-images.githubusercontent.com/13326651/219394244-7614c19c-b6a9-4a9f-b9a4-8ddf929a22d6.png)





