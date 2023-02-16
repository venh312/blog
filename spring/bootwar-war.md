## 개요
스프링부트 프로젝트를 bootwar, war로 빌드하여 내장·외장 톰캣 실행

### bootWar
내장 톰캣 실행 가능, 외장 톰캣 실행 가능

### war
내장 톰캣 실행 불가, 외장 톰캣 실행 가능

### 성능
내장·외장 성능에 대해서 유의미한 큰 차이는 없다고 한다. 하지만 외장 톰캣에서 virtual host 같은 기능의 구성 시 간단하게 적용 가능하다.

### virtual host
도메인 host에 따라 각각의 다른 루트 컨텍스트를 갖게하여 하나의 웹 애플리케이션 배포만으로 마치 여러 애플리케이션을 운영하는것처럼 하는 기능

### 패키지 구성의 차이
|bootWar|war|
|---|-------|
|WEB-INF|WEB-INF|
|META-INF|META-INF|
|org||

- bootWar의 경우, 내장 톰캣으로 단독 실행이 가능 하게 하는 WEB-INF > lib-provided 구성이 존재한다.

## 배포 실습

### 구성환경
Java 1.8, Spring Boot 2.7.8, Gradle, IntelliJ Community

### 프로젝트 환경
![1](https://user-images.githubusercontent.com/13326651/219359023-49d286aa-58bb-4fcc-b51b-3e5998617e2d.PNG)

### 테스트 컨트롤러 생성
![image](https://user-images.githubusercontent.com/13326651/219362921-90b60fff-2191-4c8f-a077-0fb0ad37e223.png)   
호출 테스트를 위해 @RestContoller로 간단한 테스트 컨트롤러를 생성한다.



