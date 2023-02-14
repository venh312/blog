## Nginx를 활용한 reverse proxy
![reverse proxy](https://user-images.githubusercontent.com/13326651/218632491-a2d02fc0-c3e0-45ce-98e5-eba8c7541710.png)

## [Nginx](https://www.nginx.com/resources/faq/)
트래픽이 많은 웹사이트의 서버(WAS)를 도와주는 비동기 이벤트 기반구조의 웹 서버 프로그램으로 공식문서에서는 "NGINX는 고성능, 확장성, 고가용성 웹서버, 역방향 프록시 서버 및 웹 가속기(HTTP 로드밸런서, 콘텐츠 캐시 등의 기능 결합)으로 소개 한다.

## Apache vs NginX
|Apache|NginX|
|------|---|
|요청 당 스레드 또는 프로세스가 처리하는 구조|비동기 이벤트 기반으로 요청|
|CPU/메모리 자원 낭비 심함|CPU/메모리 자원 사용률 낮음|
|안정성, 확장성, 호환성 우세|성능 우세|
|동적 컨텐츠 단독 처리 가능|컨텐츠 단독 처리 불가능|

## WAS
스프링부트를 이용한 임베디드 톰캣 또는 외장 톰캣을 별도로 설치해서 구성 할 수 있다.
