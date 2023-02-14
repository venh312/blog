## JAR vs WAR
class < jar < war < ear

## JAR (Java Application Archive)
- java class 파일 및 리소스파일(이미지, 텍스트 등)의 컨테이너이다.
- jar 파일이 독립실행 되려면, 클래스 중 하나가 기본 클래스로 정의된다.
- JRE(Java Runtime Environment)만 가지고도 실행이 가능하다.
- java -jar 로 실행할 수 있다.

## WAR(Web Application aRchive)
- 웹 어플리케이션을 저장하고 압축해 놓은 파일
- html, JSP, 서블릿 소스 등 배치 할 수 있는 웹 어플리케이션(Web Application) 압축 파일 포맷
- war는 WAS 위에서 돌아갈 수 있다.
- Tomcat 위에 얹어서 디플로이한다.
- WAR 파일도 JAVA의 JAR 옵션( java - jar)을 이용해 생성하는 JAR파일의 일종으로 웹어플리케이션 전체를 패키징하기 위한 jar 파일이다.
- bootWar로 패키징하면 java -jar 로 실행할 수 있다.
