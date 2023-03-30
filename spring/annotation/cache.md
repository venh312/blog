## @EnableCaching - 스프링 캐시 사용 활성화 
```java
@EnableCaching
@Configuration 
public class CacheConfig {
    ... 
}
```

## 캐시 어노테이션 종류
### @Cacheable: 캐시 저장 및 조회
캐시에 데이터가 없을 경우에는 기존의 로직을 실행한 후에 캐시에 데이터를 추가하고, 캐시에 데이터가 있으면 캐시의 데이터를 반환한다. (보통 메소드에 적용)

```java
@Cacheable("weeklyRank")
public WeeklyRank getWeeklyRank(String type) {
  ...
}
```

메소드의 파라미터 값을 기준으로 캐시한다. 위의 메소드의 경우 **type이 A로 들어왔을때 캐시되어있지 않다면 캐시에 저장하고 다음에 A로 호출될 시 캐시에서 조회된 값을 반환한다. type이 B로 들어온다면 캐시되어 있지 않아 다시 캐시에 저장한다.**

### 파라미터가 없다면 디폴트 값 0으로 저장되어 사용하며, 파라미터가 여러개일 경우 key 옵션을 사용할 수 있다.
```java
@Cacheable(value = "weeklyRank", key = "#type")
public WeeklyRank getWeeklyRank(String type, String sort) {
  ...
}
```



@CacheEvict: 캐시 제거
@CachePut: 메소드 실행을 방해하지 않고 캐시를 업데이트
@Caching: 메소드에 적용 할 여러 캐시 조작을 재 그룹화
@CacheConfig: 클래스 수준에서 몇 가지 일반적인 캐시 관련 설정을 공유






### Reference
- https://docs.spring.io/spring-boot/docs/2.1.6.RELEASE/reference/html/boot-features-caching.html
