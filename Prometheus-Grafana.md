## 모니터링 시스템 구축
스프링 부트 웹 애플리케이션을 배포한 뒤 프로메테우스, 그라파나로 모니터링 시스템을 구축한다.

## 구성환경
Windows 10, Spring Boot, Docker

## Prometheus
- Metrics를 수집하고 모니터링 및 알람에 사용되는 오픈소스 애플리케이션
- Pull 방식의 구조와 다양한 Metrics Exporter 제공
- 시계열 DB에 Metrics 저장 -> 조회 가능

## Grafana
- 데이터 시각화, 모니터링 및 분석을 위한 오픈소스 애플리케이션
- 시계열 데이터를 시각화하기 위한 대시보드 제공

## build.gradle
```bash
implementation 'org.springframework.boot:spring-boot-starter-actuator'
implementation 'io.micrometer:micrometer-registry-prometheus'
```

## build.gradle
```bash
management:
  endpoints:
    web:
      exposure:
        include: health, info, metrics, prometheus
```

## 프로메테우스(Prometheus) 설치
- **[직접 설치](https://prometheus.io/download/)**
  ![1](https://user-images.githubusercontent.com/13326651/217295919-2f318760-24bf-45ed-b9a3-7276fd0f2b29.PNG)
  
- **도커로 설치**
  - docker run -d --name=prometheus -p 9090:9090 prom/prometheus

## prometheus.yml 수정 (경로: /etc/prometheus, 윈도우는 설치 폴더에 있다.)
1. **metrics_path** 을 아래와 같이 설정한다.
2. **targets** 을 스프링부트 웹 애플리케이션으로 주소로 설정한다. 
  - 현재는 도커 기준이라 host.docker.internal로 되어있다. **예) http://localhost:8080**

```css
scrape_configs:
  - job_name: 'spring--app'
    metrics_path: '/actuator/prometheus'
    static_configs:
      - targets: ['host.docker.internal:8080']
```

## 프로메테우스 실행
**http://localhost:9090** 접속 후 **Status탭 → Targets**에 스프링부트 웹 애플리케이션이 등록되어 실행중인지 확인한다.

![image](https://user-images.githubusercontent.com/13326651/217291487-5fe14675-22d3-410b-9793-92862ff4c90e.png)

### Graph 탭으로 이동해서 jvm_memory_used_bytes 입력 후 실행(Execute)하면 메모리 사용량을 확인 할 수 있다.

<img src="https://user-images.githubusercontent.com/13326651/217292640-2762050d-8c08-4566-afc3-09996c7f3ee2.png"  width="800" height="800"/>

## 그라파나(Grafana) 설치
- **[직접 설치](https://grafana.com/grafana/download)**
  ![3](https://user-images.githubusercontent.com/13326651/217296615-f274caec-e38b-40d6-b6b5-6e58ca1034ad.PNG)
- **도커로 설치**
  - docker run -d --name=grafana -p 3000:3000 grafana/grafana

## 그라파나(Grafana) 접속 
http://localhost:3000 주소로 접속한다. **초기 계정은 admin/admin**

<img src="https://user-images.githubusercontent.com/13326651/217297538-ad49d521-fdc2-4d6d-aad0-e533644d9e55.png"  width="500" height="500"/>

## 데이터 소스 추가
<img src="https://user-images.githubusercontent.com/13326651/217303261-58b4e0f8-52c0-4535-a61e-c5d88938895a.PNG"  width="1000" height="300"/>
<img src="https://user-images.githubusercontent.com/13326651/217303285-f57482f2-ec9c-4838-a6b8-64599c159321.PNG"  width="1000" height="300"/>
<img src="https://user-images.githubusercontent.com/13326651/217303294-e7876ee2-62a6-4972-a78c-eb62f384647f.PNG"  width="1000" height="300"/>
<img src="https://user-images.githubusercontent.com/13326651/217303315-a4e9ea38-11b8-4db4-9892-a80da7d3282c.PNG"  width="1000" height="300"/>

## 대시 보드 추가
![8](https://user-images.githubusercontent.com/13326651/217305454-bf51e7bc-cca9-436b-9099-99ee8f5ac949.png)
![9](https://user-images.githubusercontent.com/13326651/217305474-dccfc2ed-87ac-44f0-954a-583bdd5eb615.PNG)
![10](https://user-images.githubusercontent.com/13326651/217305482-802180a4-1d5e-4d51-8d1a-fd85f5acbf5b.PNG)

## 대시보드
![11](https://user-images.githubusercontent.com/13326651/217305498-f38a205d-1053-4933-991c-835a578d058a.PNG)









