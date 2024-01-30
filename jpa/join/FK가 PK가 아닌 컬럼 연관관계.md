## 연관 관계 매핑 fetch join

FK가 PK가 아닌 다른 컬럼과 연관관계가 있을 때, referencedColumnName 사용한다.
(default는 연관테이블의 @Id를 바라본다.)

@ManyToOne(fetch = FetchType.LAZY)
@JoinColumn(name = "grade_code", referencedColumnName = "code")
private Grade grade;

## Exception 발생
class com.issuemoa.users.domain.grade.Grade **cannot be cast to class java.io.Serializable** (com.issuemoa.users.domain.grade.Grade is in unnamed module of loader 'app'; java.io.Serializable is in module java.base of loader 'bootstrap')

#### 해결 : 대상 클래스를 implements Serializable 한다.

### Reference
- https://hibernate.atlassian.net/browse/HHH-7668
