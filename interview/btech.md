
  ## 1. Web/Network 기본 동작 원리

  ### 1-1. HTTP/HTTPS와 API 기본

     핵심 개념:*
         HTTP(HyperText Transfer Protocol):* 웹에서 클라이언트와 서버가 데이터를 주고받기 위한 통신 규약입니다.
         HTTPS(HTTP Secure):* HTTP에 SSL/TLS 암호화 계층을 추가하여, 통신 내용을 암호화함으로써 보안을 강화한 버전입니다.
  데이터 탈취를 방지합니다.
         HTTP 메서드:* 클라이언트가 서버에 요청하는 동작의 종류를 나타냅니다.
          *   GET: 리소스 조회.
          *   POST: 리소스 생성.
          *   PUT: 리소스 전체 교체/수정.
          *   DELETE: 리소스 삭제.
         HTTP 상태 코드:* 서버가 클라이언트의 요청에 대해 어떻게 처리했는지를 나타내는 세 자리 숫자입니다.
          *   2xx (성공): 200 OK, 201 Created
          *   4xx (클라이언트 오류): 400 Bad Request, 401 Unauthorized, 404 Not Found
          *   5xx (서버 오류): 500 Internal Server Error

     ✅ 간단한 실습/과제:*
      1.  Postman 같은 API 테스트 도구로 https://jsonplaceholder.typicode.com/posts/1 에 GET 요청을 보내고, 응답 데이터와 상태
  코드를 확인해보세요.
      2.  같은 주소에 POST 요청으로 { "title": "my title", "body": "my body" } 데이터를 보내보고, 응답이 어떻게 달라지는지
  설명해보세요.

     ➡️ 예시 답변 및 풀이:*
      1.  GET 요청 결과:
             상태 코드:* 200 OK 가 반환됩니다. 이는 요청이 성공적으로 처리되었음을 의미합니다.
             응답 데이터 (Body):* 아래와 같은 JSON 형식의 게시글 데이터가 반환됩니다.
              `json
              {
                "userId": 1,
                "id": 1,
                "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
                "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas
   totam\nnostrum rerum est autem sunt rem eveniet architecto"
              }

  `
      2.  POST 요청 결과:
             상태 코드:* 201 Created 가 반환됩니다. 이는 요청이 성공하여 서버에 새로운 리소스가 생성되었음을 의미합니다.
             응답 데이터 (Body):* 우리가 보낸 데이터에 서버가 생성한 id 값이 추가되어 반환됩니다.
              `json
              {
                "title": "my title",
                "body": "my body",
                "id": 101
              }

  `

  ### 1-2. RESTful API

     핵심 개념:*
         REST(Representational State Transfer):* 웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일입니다.
         핵심 원칙:*
          1.  자원(Resource) 중심의 URI: 모든 자원은 고유한 URI를 가져야 하며, URI는 동사가 아닌 명사로 표현합니다. (e.g.,
  /users/1)
          2.  행위(Verb)는 HTTP 메서드로 표현: 자원에 대한 행위는 GET, POST, PUT, DELETE 등의 HTTP 메서드로 표현합니다.
          3.  표현(Representation): 클라이언트와 서버는 JSON, XML 등의 형태로 데이터를 주고받습니다.
          4.  상태 없음(Stateless): 서버는 클라이언트의 상태를 저장하지 않습니다. 각 요청은 독립적으로 처리됩니다.

     ✅ 간단한 실습/과제:*
      *   '쇼핑몰의 상품(Product)'에 대한 CRUD 기능을 처리하는 RESTful API 엔드포인트 5개를 설계해보세요.

     ➡️ 예시 답변 및 풀이:*

  | 기능 | HTTP 메서드 | URI | 설명 |
  | --- | --- | --- | --- |
  | 상품 목록 조회 | GET | /products | 모든 상품의 목록을 조회합니다. |
  | 특정 상품 조회 | GET | /products/{id} | 특정 ID를 가진 상품의 정보를 조회합니다. |
  | 새 상품 등록 | POST | /products | 새로운 상품을 등록합니다. |
  | 상품 정보 수정 | PUT | /products/{id} | 특정 ID를 가진 상품의 정보를 전체 수정합니다. |
  | 상품 삭제 | DELETE | /products/{id} | 특정 ID를 가진 상품을 삭제합니다. |

  ---

  ## 2. 데이터베이스 (Database)

  ### 2-1. CRUD와 SQL

     핵심 개념:*
         CRUD:* 데이터베이스의 4가지 기본 연산. Create(생성), Read(읽기), Update(갱신), Delete(삭제).
         SQL(Structured Query Language):* 관계형 데이터베이스와 통신하기 위한 언어.

     ✅ 간단한 실습/과제:*
      *   Guestbook (방명록) 테이블에 대한 CRUD SQL문을 각각 작성해보세요.

     ➡️ 예시 답변 및 풀이:*
         Create (생성):*
          `sql
          INSERT INTO Guestbook (writer, content) VALUES ('손님1', '안녕하세요. 처음 방문합니다.');

  `
         Read (읽기):*
          `sql
          -- 모든 방명록 조회
          SELECT * FROM Guestbook;
          -- ID가 1인 방명록만 조회
          SELECT * FROM Guestbook WHERE id = 1;
          `
         Update (갱신):*
          `sql
          UPDATE Guestbook SET content = '내용을 수정합니다.' WHERE id = 1;
          `
         Delete (삭제):*
          `sql
          DELETE FROM Guestbook WHERE id = 1;

  `

  ### 2-2. 관계형 데이터베이스(RDB) 설계

     핵심 개념:*
         PK (Primary Key):* 테이블에서 각 행(레코드)을 고유하게 식별하는 키.
         FK (Foreign Key):* 한 테이블의 필드가 다른 테이블의 PK를 참조하여 테이블 간의 관계를 맺는 키.
         Join:* 두 개 이상의 테이블을 연결하여 데이터를 검색하는 방법.
         Index:* SELECT 쿼리의 검색 속도를 높이기 위한 자료구조. 쓰기(INSERT, UPDATE, DELETE) 성능은 저하될 수 있습니다.

     ✅ 간단한 실습/과제:*
      *   '사용자(User)'와 '게시글(Post)' 테이블을 1:N 관계로 설계해보세요.

     ➡️ 예시 답변 및 풀이:*
      `sql
      -- 사용자 테이블
      CREATE TABLE User (
          id BIGINT PRIMARY KEY AUTO_INCREMENT,
          username VARCHAR(255) NOT NULL UNIQUE,
          email VARCHAR(255) NOT NULL UNIQUE
      );


      -- 게시글 테이블
      CREATE TABLE Post (
          id BIGINT PRIMARY KEY AUTO_INCREMENT,
          title VARCHAR(255) NOT NULL,
          content TEXT,
          user_id BIGINT, -- 작성자의 ID를 저장할 컬럼
          FOREIGN KEY (user_id) REFERENCES User(id) -- User 테이블의 id를 참조하는 외래 키
      );

  `
      *   Post 테이블의 user_id가 User 테이블의 id를 참조함으로써, '한 명의 User는 여러 개의 Post를 작성할 수 있다'는 1:N
  관계가 형성됩니다.

  ### 2-3. 트랜잭션 (Transaction)

     핵심 개념:*
         트랜잭션:* 데이터베이스의 상태를 변화시키는 하나의 논리적 작업 단위.
         ACID 원칙:*
             원자성(Atomicity):* 모두 성공하거나 모두 실패해야 함.
             일관성(Consistency):* 트랜잭션 후에도 데이터베이스는 일관된 상태를 유지해야 함.
             고립성(Isolation):* 한 트랜잭션이 다른 트랜잭션에 영향을 주지 않고 독립적으로 실행되어야 함.
             지속성(Durability):* 성공한 트랜잭션의 결과는 영구적으로 저장되어야 함.

     ✅ 간단한 실습/과제:*
      *   'A 계좌에서 10,000원 출금, B 계좌로 입금' 시나리오에서 트랜잭션이 왜 필요한지 설명해보세요.

     ➡️ 예시 답변 및 풀이:*
      이체 과정은 1) A 계좌 잔액 감소, 2) B 계좌 잔액 증가의 두 단계로 이루어집니다.
      만약 1번 단계 성공 후, 2번 단계 직전에 시스템 장애가 발생하면 A의 돈은 사라지고 B에게는 입금되지 않는 심각한 문제가
  발생합니다.
      트랜잭션은 이 두 단계를 하나의 묶음(원자성)으로 처리하여, 중간에 실패하면 모든 작업을 없던 일(Rollback)로 되돌립니다.
  이를 통해 돈이 사라지는 일 없이 데이터의 일관성을 보장할 수 있습니다.

  ---

  ## 3. 서버 프레임워크 (예: Spring Boot)

  ### 3-1. 서버의 기본 구조 (MVC 패턴)

     핵심 개념:*
      *   애플리케이션을 Model, View, Controller 세 가지 역할로 구분하는 디자인 패턴. 백엔드에서는 주로 API 서버를 만드므로
  View를 제외하고 생각합니다.
             Controller:* HTTP 요청을 받고, 요청에 맞는 Service를 호출.
             Service:* 비즈니스 로직(실제 기능)을 수행.
             Repository:* 데이터베이스에 접근하여 데이터를 저장/조회.

     ✅ 간단한 실습/과제:*
      *   Spring Boot의 @RestController, @Service, @Repository가 MVC 패턴의 어느 부분에 해당하며, 왜 역할을 나누는지
  설명해보세요.

     ➡️ 예시 답변 및 풀이:*
         `@RestController`: Controller*에 해당. 클라이언트의 HTTP 요청을 직접 받는 관문 역할.
         `@Service`: Service*에 해당. Controller로부터 요청을 받아 실제 비즈니스 로직을 처리.
         `@Repository`: Repository*에 해당. Service의 요청에 따라 DB의 데이터를 CRUD.
         역할을 나누는 이유:* 각자의 책임과 관심사를 분리(Separation of Concerns)하기 위함입니다. 이를 통해 코드가 명확해지고,
  단위 테스트가 용이해지며, 유지보수성이 크게 향상됩니다.

  ### 3-2. ORM (Object-Relational Mapping, 예: JPA)

     핵심 개념:*
         ORM:* 객체(Object)와 관계형 데이터베이스(Relational)를 자동으로 매핑(Mapping)해주는 기술. SQL을 직접 작성하지 않고
  객체를 통해 DB를 조작할 수 있게 합니다.
         N+1 문제:* 연관 관계가 있는 엔티티 조회 시, 첫 쿼리(1) 이후 연관된 엔티티를 가져오기 위해 N개의 추가 쿼리가 발생하는
  성능 저하 문제.

     ✅ 간단한 실습/과제:*
      *   위에서 설계한 User와 Post 테이블을 JPA의 @Entity를 사용하여 클래스로 정의해보세요.

     ➡️ 예시 답변 및 풀이:*
      `java
      // User.java
      import javax.persistence.*;
      import java.util.ArrayList;
      import java.util.List;


      @Entity
      public class User {
          @Id
          @GeneratedValue(strategy = GenerationType.IDENTITY)
          private Long id;
          private String username;

          @OneToMany(mappedBy = "user") // Post의 'user' 필드와 매핑됨
          private List<Post> posts = new ArrayList<>();

          // Getters and Setters
      }

      // Post.java
      import javax.persistence.*;


      @Entity
      public class Post {
          @Id
          @GeneratedValue(strategy = GenerationType.IDENTITY)
          private Long id;
          private String title;

          @ManyToOne // 다대일 관계
          @JoinColumn(name = "user_id") // 외래 키
          private User user;

          // Getters and Setters
      }

  `

  ---

  ## 4. 인증과 인가 (Authentication & Authorization)

  ### 4-1. 인증 방식

     핵심 개념:*
         인증(Authentication):* 당신이 누구인지 확인하는 과정 (e.g., 로그인).
         인가(Authorization):* 당신이 무엇을 할 수 있는지 권한을 확인하는 과정 (e.g., 관리자 페이지 접근).
         세션/쿠키:* 서버가 사용자 정보를 저장하고, 클라이언트에게는 식별자(세션 ID)만 쿠키로 보내는 방식. 서버 부하가 있을 수
  있음.
         토큰(JWT):* 사용자 정보를 암호화한 토큰 자체를 클라이언트에게 발급. 서버는 상태를 저장하지 않아(Stateless) 확장성이
  좋음.

     ✅ 간단한 실습/과제:*
      *   JWT의 구조를 설명하고, 서버가 JWT를 검증하는 과정을 설명해보세요.

     ➡️ 예시 답변 및 풀이:*
         구조:* .으로 구분된 세 부분(Header, Payload, Signature)으로 구성됩니다.
          1.  Header: 토큰 타입(JWT)과 서명 알고리즘(HS256 등) 정보.
          2.  Payload: 실제 담을 정보(사용자 ID, 이름, 만료 시간 등).
          3.  Signature: Header와 Payload를 합친 후, 서버의 비밀 키로 암호화한 값. 토큰의 위변조 여부를 확인하는 데 사용.
         검증 과정:*
          1.  클라이언트가 요청 시 헤더에 Authorization: Bearer <token> 형태로 JWT를 담아 보냅니다.
          2.  서버는 받은 JWT의 Header와 Payload를 가져와, 자신이 가진 비밀 키로 Signature를 다시 계산합니다.
          3.  새로 계산한 Signature와 받은 JWT의 Signature가 일치하는지 비교합니다.
          4.  일치하면 위변조되지 않은 유효한 토큰으로 신뢰하고, Payload의 만료 시간(exp) 등을 추가로 확인하여 인가를
  처리합니다.

  ### 4-2. 비밀번호 암호화

     핵심 개념:*
         해싱(Hashing):* 임의의 길이 데이터를 고정된 길이의 데이터로 매핑하는 단방향 함수. 원본 값을 복호화할 수 없습니다.
         Salting:* 해싱 전 원본 비밀번호에 임의의 문자열(Salt)을 추가하여, 같은 비밀번호라도 다른 해시 값이 나오게 하는 기법.
  레인보우 테이블 공격을 방지합니다.
         Bcrypt:* Salting과 Key Stretching(해시 함수 반복)을 적용하여 의도적으로 해시 계산 속도를 늦춘, 비밀번호 저장에 특화된
  알고리즘.

     ✅ 간단한 실습/과제:*
      *   회원가입 시 사용자가 입력한 비밀번호를 안전하게 DB에 저장하기 위한 전체 프로세스를 설명해보세요.

     ➡️ 예시 답변 및 풀이:*
      1.  클라이언트로부터 사용자 ID와 평문 비밀번호를 전달받습니다.
      2.  서버는 Bcrypt와 같은 안전한 라이브러리를 사용하여 비밀번호를 해싱합니다. 이 과정에서 Salt가 자동으로 생성되고
  적용됩니다.
      3.  데이터베이스의 User 테이블에는 사용자 ID와 해싱된 비밀번호를 저장합니다. 절대 평문 비밀번호를 저장하지 않습니다.
      4.  로그인 시에는, 클라이언트로부터 받은 평문 비밀번호와 DB에 저장된 해싱된 비밀번호를 Bcrypt 라이브러리의 matches 같은
  검증 함수로 비교합니다. 이 함수는 내부적으로 저장된 해시 값의 Salt를 사용하여 입력된 비밀번호를 다시 해싱한 후 일치 여부를
  판단해줍니다.
