## Java 11
- Spring에 새로운 메소드 추가
- Files 클래스에 새로운 메소드 추가
- 컬렉션 인터페이스에 새로운 메소드 추가
- Predicate 인터페이스에 새로운 메소드 추가
- 람다에서 로컬 변수 Var 사용
- 자바 파일 실행 방식 단순화

### String 클래스에 새로운 6가지 메소드가 추가
- strip(): 문자열 앞, 뒤의 공백 제거.
- stripLeading(): 문자열 앞의 공백 제거.
- stripTrailing(): 문자열 뒤의 공백 제거.
- isBlank(): 문자열이 비어있거나, 공백만 포함되어 있을 경우 true를 반환한다.
- String.trim().isEmpty() 와 결과가 동일함.
- repeat(n): n개만큼 문자열을 반복하여 붙여서 반환함.
 

### java.nio.file.Files 클래스에 새로운 3가지 메소드가 추가
- Path writeString(Path, String, Charset, OpenOption): 파일에 문자열을 작성하고 Path로 반환한다. 파일 오픈 옵션에 따라 작동 방식을 달리하며, charset을 지정하지 않으면 UTF-8이 사용된다.
- String readString(Path, Charset): 파일 전체 내용을 읽어서 String으로 반환하고, 파일 내용을 모두 읽거나 예외가 발생하면 알아서 close를 한다. charset을 지정하지 않으면 UTF-8이 사용된다.
- boolean isSameFile(Path, Path): 두 Path가 같은 파일을 가리키며, true, 아니면 false를 반환한다.
 

### 컬렉션 인터페이스에 새로운 메소드 추가
컬렉션의 toArray() 메소드를 오버 로딩하는 메소드가 추가되었고, 원하는 타입의 배열을 선택하여 반환할 수 있게 되었다.

- List sampleList = Arrays.asList("Java", "Kotlin"); 
- String[] sampleArray = sampleList.toArray(String[]::new); 
- assertThat(sampleArray).containsExactly("Java", "Kotlin");
 

Predicate 인터페이스에 새로운 메소드 추가
Predicate 인터페이스에 부정을 나타내는 not() 메소드가 추가되었다.

 

List<String> sampleList = Arrays.asList("Java", "\n \n", "Kotlin", " "); 
List withoutBlanks = sampleList.stream() 
 .filter(Predicate.not(String::isBlank))
 .collect(Collectors.toList()); 
assertThat(withoutBlanks).containsExactly("Java", "Kotlin");
 

람다에서 로컬 변수 Var 사용
람다식에서 Var을 사용할 수 있게 되었다.

 

List<String> sampleList = Arrays.asList("Java", "Kotlin"); 
String resultString = sampleList.stream() 
.map((@Nonnull var x) -> x.toUpperCase()) 
.collect(Collectors.joining(", ")); 
assertThat(resultString).isEqualTo("JAVA, KOTLIN");
 

자바 파일 실행
javac를 통해 컴파일 하지 않고도, 바로 java 파일을 실행할 수 있게 되었다.

 

// Java 11 이전
$ javac HelloWorld.java
$ java Helloworld
Hello Java 8!

// Java 11 이후
$ java HelloWorld.java
Hello Java 11!
 

Garbage Collector
Java 11의 Default GC는 G1 GC이다.
