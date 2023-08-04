Java 11에서 도입된 HTTP/2 지원은 웹 프로토콜에서 큰 개선을 가져왔습니다. 
HTTP/2는 이전 버전인 HTTP/1.1과 비교하여 성능과 효율성을 크게 향상시킨 프로토콜입니다. 이를 위해 다음과 같은 주요 개선 사항이 포함되어 있습니다:

1. **다중화 및 스트림**: HTTP/2는 하나의 TCP 연결을 통해 여러 개의 스트림을 동시에 처리하는 다중화 기능을 제공합니다. 이로써 여러 요청과 응답을 한 연결로 동시에 처리하여 네트워크 리소스의 효율성을 높입니다.
2. **헤더 압축**: HTTP/1.1에서는 헤더 필드가 중복해서 전송되어 대역폭 낭비가 발생할 수 있었습니다. HTTP/2는 헤더 필드를 압축하여 전송하므로 헤더 정보의 크기를 줄여 네트워크 사용량을 최소화합니다.
3. **서버 푸시**: HTTP/2에서는 서버가 클라이언트의 요청에 대해 해당 리소스와 함께 관련 리소스도 함께 보낼 수 있는 "서버 푸시" 기능을 제공합니다. 이를 통해 클라이언트가 추가 요청을 하지 않고도 필요한 리소스를 미리 받을 수 있습니다.

Java 11에서는 HTTP/2를 지원하기 위해 새로운 `java.net.http` 패키지가 도입되었습니다.
이 패키지에는 HTTP 클라이언트 API가 포함되어 HTTP/1.1 및 HTTP/2를 모두 지원하며, 비동기 및 동기식 요청을 처리할 수 있습니다. 이를 통해 개발자들은 HTTP 요청 및 응답을 보다 쉽게 처리하고 더욱 효율적으로 관리할 수 있습니다.

`java.net.http` 패키지의 주요 클래스와 인터페이스:

- `HttpClient`: HTTP 클라이언트의 엔트리 포인트로, 요청을 보내고 응답을 받는 역할을 합니다.
- `HttpRequest`: HTTP 요청을 정의하는 클래스로, 요청 메서드, 헤더, 본문 등을 설정할 수 있습니다.
- `HttpResponse`: HTTP 응답을 나타내는 클래스로, 응답 코드, 헤더, 본문 등을 처리할 수 있습니다.

### Java 11에서 `java.net.http` 패키지를 사용한 간단한 예제 코드입니다:
```java
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class Main {
    public static void main(String[] args) throws Exception {
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
                .uri(new URI("https://www.example.com"))
                .build();
        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
        
        System.out.println("Response Code: " + response.statusCode());
        System.out.println("Response Body: " + response.body());
    }
}
```

### Java 8에서 사용하던 코드
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
    public static void main(String[] args) throws Exception {
        String urlString = "https://www.example.com";
        URL url = new URL(urlString);
        
        HttpURLConnection connection = (HttpURLConnection) url.openConnection();
        connection.setRequestMethod("GET");
        
        int responseCode = connection.getResponseCode();
        System.out.println("Response Code: " + responseCode);
        
        BufferedReader reader = new BufferedReader(new InputStreamReader(connection.getInputStream()));
        String inputLine;
        StringBuffer response = new StringBuffer();
        
        while ((inputLine = reader.readLine()) != null) {
            response.append(inputLine);
        }
        reader.close();
        
        System.out.println("Response Body: " + response.toString());
    }
}
```

이렇게 Java 11에서 제공하는 `java.net.http` 패키지를 사용하면 더 효율적이고 간단하게 HTTP 요청 및 응답을 처리할 수 있습니다.

