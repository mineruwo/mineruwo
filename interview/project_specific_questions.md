### **프로젝트 기반 면접 예상 질문**

이 문서는 `Idle_React_Project` (NaviLogistics)와 `Team_project_full_stack` (가상 쇼핑몰) 프로젝트 경험에 기반한 심층 면접 질문 목록입니다.

---

### **1. Idle_React_Project (NaviLogistics - 화물 운송 플랫폼)**

#### **1.1. 아키텍처 및 설계**

<details>
<summary>이 프로젝트에서 풀스택 개발자 및 PM 역할을 동시에 수행하셨습니다. 기술 스택으로 Spring Boot와 React를 선택한 주된 이유는 무엇이었나요? 다른 기술 스택(e.g., Node.js, Vue.js)과 비교했을 때 어떤 장점이 있다고 판단하셨습니까?</summary>
<p>

**답변 예시:**
"네, 저희 팀은 안정성과 생산성을 모두 고려하여 기술 스택을 결정했습니다.

**백엔드로 Spring Boot를 선택한 이유**는 다음과 같습니다.
1.  **안정성과 생태계:** Java와 Spring 프레임워크는 오랜 기간 수많은 대규모 서비스에서 검증되어 안정성이 매우 높습니다. Spring Security, JPA, WebSocket 등 프로젝트에 필요한 대부분의 기능들을 공식적으로 지원하는 강력한 생태계 덕분에 개발에만 집중할 수 있었습니다.
2.  **팀원 역량:** 팀원 대부분이 Java에 익숙했기 때문에, 학습 곡선을 최소화하고 빠르게 개발을 시작할 수 있다는 장점이 있었습니다.

**프론트엔드로 React를 선택한 이유**는 다음과 같습니다.
1.  **컴포넌트 기반 아키텍처:** 물류 플랫폼의 복잡한 UI(관리자 대시보드, 실시간 지도 등)를 재사용 가능한 컴포넌트 단위로 개발하고 관리하는 데 매우 효율적이라 판단했습니다.
2.  **거대한 커뮤니티와 자료:** 개발 중 마주치는 문제에 대한 해결책이나 라이브러리를 찾기 용이하여 생산성을 높일 수 있었습니다.

Node.js 기반의 스택도 고려했지만, 복잡한 비즈니스 로직과 데이터 무결성이 중요한 저희 프로젝트 특성상, 정적 타입 언어인 Java와 성숙한 프레임워크인 Spring Boot가 장기적인 안정성과 유지보수성 측면에서 더 적합하다고 최종적으로 판단했습니다."

</p>
</details>

<details>
<summary>프론트엔드 상태 관리 라이브러리로 Redux Toolkit을 사용하셨습니다. 어떤 상황에서 Redux의 필요성을 느끼셨나요? 예를 들어, props drilling으로 해결하기 어려웠던 특정 상태 관리 문제가 있었나요?</summary>
<p>

**답변 예시:**
"초기에는 React의 `useState`와 Context API를 이용해 상태를 관리했습니다. 하지만 애플리케이션 규모가 커지면서 여러 컴포넌트가 공통으로 사용하는 상태(e.g., 로그인한 사용자 정보, 실시간 운송 오더 목록)가 많아졌고, 이로 인해 심각한 'props drilling' 문제를 겪게 되었습니다.

예를 들어, 최상위 컴포넌트에서 API로 받아온 사용자 정보를 4~5단계 아래의 자식 컴포넌트로 전달해야 하는 경우가 빈번했습니다. 이는 코드의 가독성을 해치고 유지보수를 어렵게 만들었습니다.

이 문제를 해결하기 위해 전역 상태 관리의 필요성을 느꼈고, Redux Toolkit을 도입했습니다. Redux Toolkit은 기존 Redux의 단점이었던 복잡한 설정과 많은 보일러플레이트 코드를 `createSlice`와 같은 유틸 함수로 크게 줄여주었습니다. 덕분에 중앙 집중화된 저장소(store)에서 상태를 효율적으로 관리할 수 있었고, 컴포넌트 구조를 훨씬 깔끔하게 유지할 수 있었습니다."

</p>
</details>

<details>
<summary>ERD를 보면 `CUSTOMER` 테이블이 화주와 차주의 역할을 모두 겸하는 구조로 보입니다. 이렇게 단일 테이블로 설계했을 때의 장점과 단점은 무엇이라고 생각하시나요? 만약 테이블을 분리했다면 어떤 점이 달라졌을까요?</summary>
<p>

**답변 예시:**
"네, 초기 설계 단계에서 사용자 관리의 단순화를 위해 `CUSTOMER` 테이블에 `ROLE` 컬럼을 두어 화주와 차주를 구분하는 단일 테이블 전략을 선택했습니다.

**장점**은 명확했습니다. 회원가입, 로그인, 프로필 관리 등 공통된 사용자 관리 로직을 하나로 통일할 수 있어 개발 초기 생산성이 높았습니다.

하지만 **단점**도 있었습니다. 프로젝트가 진행되면서 차주에게만 필요한 정보(e.g., 운전면허, 차량 정보)와 화주에게만 필요한 정보(e.g., 사업자등록번호)가 늘어나면서 `CUSTOMER` 테이블에 null 값을 허용하는 컬럼이 많아졌습니다. 또한, 차주와 화주의 상태나 로직이 달라질수록 `ROLE`에 따른 분기 처리가 서비스 계층 코드에 많아져 복잡성이 증가했습니다.

만약 다시 설계한다면, 공통 정보를 담는 `USER` 테이블을 두고, `SHIPPER_PROFILE`과 `DRIVER_PROFILE` 테이블을 만들어 1:1 관계로 연결하는 방식을 고려할 것 같습니다. 이렇게 하면 각 도메인의 역할과 데이터가 명확하게 분리되어 확장성과 유지보수성 측면에서 더 나은 구조가 되었을 것이라 생각합니다."

</p>
</details>

#### **1.2. 담당 역할: DevOps**

<details>
<summary>`render.yaml` 파일을 보면 React 프론트엔드에 대한 배포 설정(Static Site)만 정의되어 있습니다. Spring Boot 백엔드는 어떤 방식으로 배포하셨나요? Render의 다른 서비스 타입(e.g., Web Service)을 사용하셨다면, 그 과정과 설정에 대해 설명해주세요.</summary>
<p>

**답변 예시:**
"네, 좋은 질문입니다. 저장소에 있는 `render.yaml`은 프론트엔드 배포만을 위한 설정입니다. 저희는 백엔드와 프론트엔드를 별도의 서비스로 분리하여 배포했습니다.

Spring Boot 백엔드는 Render의 **'Web Service'** 타입으로 배포했습니다. 설정 과정은 다음과 같았습니다.
1.  Render 대시보드에서 새로운 'Web Service'를 생성하고, 동일한 GitHub 저장소를 연결했습니다.
2.  **`Root Directory`** 옵션을 `backend/backend_idle`로 지정하여 백엔드 소스 코드 위치를 명시했습니다.
3.  **`Build Command`**는 `./gradlew build -x test`로 설정하여 테스트를 제외한 빌드를 수행했습니다.
4.  **`Start Command`**는 `java -jar build/libs/backend_idle-0.0.1-SNAPSHOT.jar`로 설정하여 빌드된 JAR 파일을 실행하도록 했습니다.

이렇게 두 개의 서비스를 분리하여 배포함으로써, 프론트엔드와 백엔드의 배포 라이프사이클을 독립적으로 관리할 수 있었고, 각 환경에 맞는 최적화된 설정을 적용할 수 있었습니다."

</p>
</details>

<details>
<summary>프로덕션 환경에서 프론트엔드가 백엔드 API를 호출할 때, API 엔드포인트 주소는 어떻게 관리하셨나요? (e.g., 환경 변수, 프록시 설정 등)</summary>
<p>

**답변 예시:**
"API 엔드포인트는 **환경 변수**를 사용하여 관리했습니다.

로컬 개발 환경에서는 프론트엔드 프로젝트 루트에 `.env.development` 파일을 만들어 `REACT_APP_API_URL=http://localhost:8080`과 같이 백엔드 주소를 설정했습니다. React는 `REACT_APP_` 접두사가 붙은 환경 변수를 자동으로 인식하여 `process.env.REACT_APP_API_URL` 형태로 코드 내에서 사용할 수 있게 해줍니다.

프로덕션 배포 시에는 Render의 프론트엔드 서비스 설정에서 동일한 이름의 환경 변수(`REACT_APP_API_URL`)를 추가하고, 값으로 실제 배포된 백엔드 서비스의 주소(`https://idle-react-project-backend.onrender.com`)를 입력했습니다.

이 방식을 통해 소스 코드를 수정하지 않고도 개발 환경과 프로덕션 환경에서 각각 다른 API 서버를 바라보도록 유연하게 설정할 수 있었습니다."

</p>
</details>

<details>
<summary>`README.md`에 Docker가 기술 스택으로 포함되어 있는데, 이 프로젝트에서 Docker는 어떤 용도로 사용되었나요? 로컬 개발 환경을 구성하는 데 사용되었나요, 아니면 배포 과정의 일부였나요?</summary>
<p>

**답변 예시:**
"이 프로젝트에서 Docker는 주로 **로컬 개발 환경을 표준화**하고, 팀원들이 **개발에 빠르게 참여**할 수 있도록 돕는 용도로 사용되었습니다.

프로젝트 루트에 `docker-compose.yml` 파일을 작성하여, Spring Boot 백엔드 애플리케이션과 Supabase에서 사용하는 것과 동일한 버전의 PostgreSQL 데이터베이스를 서비스로 정의했습니다. 덕분에 새로운 팀원이 프로젝트에 합류했을 때, 자신의 컴퓨터에 Java, Gradle, PostgreSQL을 각각 설치하는 복잡한 과정 없이 `docker-compose up` 명령어 한 번으로 전체 백엔드 개발 환경을 즉시 실행할 수 있었습니다.

이를 통해 모든 팀원이 동일한 환경에서 개발을 진행함으로써 "제 PC에서는 되는데..."와 같은 문제를 원천적으로 방지하고 개발 생산성을 높일 수 있었습니다. 배포는 Render의 네이티브 환경을 사용했기 때문에, 배포 과정에 직접적으로 Docker가 사용되지는 않았습니다."

</p>
</details>

#### **1.3. 담당 역할: 관리자 페이지 및 실시간 채팅 (Backend)**

<details>
<summary>실시간 채팅 기능을 위해 Spring Boot에서 WebSocket과 STOMP를 사용하셨습니다. STOMP 프로토콜을 사용함으로써 얻는 이점은 무엇이었나요? 단순 WebSocket만 사용했을 때와 비교해서 설명해주세요.</summary>
<p>

**답변 예시:**
"단순 WebSocket은 양방향 통신 채널을 제공할 뿐, 메시지의 형식이나 흐름에 대한 규약이 없는 저수준 프로토콜입니다. 따라서 '누가 누구에게 메시지를 보내는지', '메시지의 목적지가 어디인지' 등을 개발자가 직접 구현해야 합니다.

저희는 이 복잡성을 줄이기 위해 WebSocket 위에서 동작하는 상위 프로토콜인 **STOMP**를 도입했습니다. STOMP를 사용함으로써 얻은 가장 큰 이점은 **메시징 구조를 체계화**할 수 있었다는 점입니다.

- **Publish/Subscribe 모델:** STOMP는 `/topic/..`이나 `/queue/..`와 같은 'destination(목적지)' 개념을 제공합니다. 클라이언트는 특정 목적지를 구독(subscribe)하고, 서버나 다른 클라이언트는 해당 목적지로 메시지를 발행(publish)하는 구조를 쉽게 만들 수 있습니다.
- **메시지 브로커:** Spring의 STOMP 지원은 내장 메시지 브로커를 통해 이 모든 과정을 처리해줍니다. 덕분에 저희는 메시지 라우팅과 같은 하위 레벨의 구현에 신경 쓰지 않고, `@MessageMapping` 어노테이션을 사용해 비즈니스 로직에만 집중할 수 있었습니다."

</p>
</details>

<details>
<summary>1:1 채팅을 구현할 때, 특정 사용자에게만 메시지를 보내는 로직은 어떻게 구현하셨나요? (e.g., `/user/{username}/queue/messages`와 같은 STOMP의 user-destination 기능 사용 여부)</summary>
<p>

**답변 예시:**
"네, 말씀하신 대로 Spring Security와 STOMP가 제공하는 **user-destination 기능**을 적극적으로 활용하여 1:1 채팅을 구현했습니다.

전체적인 흐름은 다음과 같았습니다.
1.  사용자가 웹소켓에 연결하면, Spring Security를 통해 인증된 사용자의 `Principal` 객체가 웹소켓 세션과 연결됩니다.
2.  클라이언트는 각자 자신의 고유한 메시지 큐를 구독합니다. 예를 들어, `stompClient.subscribe('/user/queue/private')`와 같은 코드로 자신의 private 큐를 구독합니다.
3.  A 사용자가 B 사용자에게 메시지를 보낼 때는, `@MessageMapping`이 설정된 컨트롤러의 특정 엔드포인트(e.g., `/app/private-chat/{recipientUsername}`)로 메시지를 전송합니다.
4.  컨트롤러 메소드에서는 메시지를 받은 후, `SimpMessagingTemplate`의 `convertAndSendToUser()` 메소드를 사용합니다. 이 메소드에 수신자(B)의 username과 목적지(`/queue/private`), 그리고 메시지 내용을 담아 호출하면, Spring이 알아서 해당 사용자의 세션을 찾아 개인화된 목적지로 메시지를 전달해줍니다. 

이 방식을 통해, 모든 메시지가 공개된 topic으로 가는 것이 아니라 특정 사용자에게만 안전하게 전달되는 1:1 채팅을 구현할 수 있었습니다."

</p>
</details>

<details>
<summary>관리자 페이지의 인증/인가는 Spring Security를 통해 어떻게 구현하셨나요? 예를 들어, 특정 URL 접근 시 'ADMIN' 역할을 가진 사용자만 접근할 수 있도록 설정하는 구체적인 방법(e.g., `SecurityFilterChain` 설정)에 대해 설명해주세요.</summary>
<p>

**답변 예시:**
"관리자 페이지의 접근 제어는 Spring Security의 **`SecurityFilterChain`**을 통해 구현했습니다.

`SecurityConfig` 클래스에 `SecurityFilterChain` 타입의 Bean을 등록하고, `http.authorizeHttpRequests()` 메소드를 사용하여 URL 패턴별로 접근 권한을 설정했습니다.

구체적인 코드는 다음과 유사합니다.
```java
@Bean
public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
    http
        .authorizeHttpRequests(authz -> authz
            .requestMatchers("/api/admin/**").hasRole("ADMIN") // /api/admin/으로 시작하는 모든 요청은 ADMIN 역할이 필요
            .requestMatchers("/api/mypage/**").hasAnyRole("USER", "ADMIN") // 마이페이지는 USER 또는 ADMIN
            .anyRequest().permitAll() // 그 외 모든 요청은 허용
        );
    // ... 기타 JWT 필터, 로그인 설정 등
    return http.build();
}
```

이렇게 설정함으로써, `/api/admin/`으로 시작하는 모든 API 요청은 JWT 토큰 필터를 거쳐 인증된 사용자의 역할(Authority)을 확인하고, 'ROLE_ADMIN'을 가진 사용자가 아닐 경우 403 Forbidden 에러를 반환하도록 하여 관리자 페이지를 보호했습니다."

</p>
</details>

#### **1.4. 담당 역할: 관리자 페이지 및 실시간 채팅 (Frontend)**

<details>
<summary>`adminPage/AdminPage.js` 컴포넌트에서 가장 복잡했던 기능은 무엇이었나요? 예를 들어, 수많은 데이터를 테이블 형태로 보여주고, 필터링 및 페이지네이션을 구현할 때 어떤 어려움이 있었고 어떻게 해결하셨나요?</summary>
<p>

**답변 예시:**
"관리자 페이지에서 가장 복잡했던 기능은 **서버사이드 페이지네이션과 동적 필터링/정렬 기능이 결합된 데이터 테이블**을 구현하는 것이었습니다.

**어려웠던 점:**
처음에는 클라이언트 사이드에서 모든 데이터를 한 번에 받아와 처리하려고 했습니다. 하지만 데이터가 수천 건 이상으로 늘어나자 초기 로딩 시간이 매우 길어졌고, 브라우저가 느려지는 문제가 발생했습니다. 또한, 여러 필터 조건(날짜, 상태, 검색어 등)이 동시에 적용될 때 상태 관리가 매우 복잡해졌습니다.

**해결 방법:**
이 문제를 해결하기 위해 **서버사이드 페이지네이션**으로 전환했습니다. 
1.  프론트엔드에서는 현재 페이지 번호, 페이지 당 아이템 수, 정렬 기준, 필터 조건 등을 상태(state)로 관리했습니다.
2.  이 상태들이 변경될 때마다, 해당 정보들을 쿼리 파라미터로 담아 백엔드 API(`/api/admin/orders?page=1&size=10&sort=createdAt,desc&status=COMPLETED`)를 호출했습니다.
3.  백엔드는 이 파라미터를 받아 JPA의 `Pageable` 객체로 변환하여 데이터베이스에서 해당 페이지의 데이터만 조회한 후, 전체 데이터 수(total elements)와 함께 프론트엔드로 전달했습니다.
4.  프론트엔드는 응답받은 데이터와 전체 데이터 수를 사용하여 테이블과 페이지네이션 UI를 렌더링했습니다. 

이 방식을 통해 초기 로딩 성능을 크게 개선하고, 클라이언트의 부담을 줄일 수 있었습니다."

</p>
</details>

<details>
<summary>`websocket/WebSocketTestPage.js` 파일이 존재하는데, 실제 채팅 UI는 어떤 컴포넌트에서 구현되었나요? `Stomp.js` 라이브러리를 사용하여 서버와 연결하고, 메시지를 구독(subscribe) 및 발행(publish)하는 코드의 흐름을 설명해주세요.</summary>
<p>

**답변 예시:**
"`WebSocketTestPage.js`는 개발 초기 단계에서 웹소켓 연결을 테스트하기 위해 만든 페이지였습니다. 실제 채팅 UI는 **`layouts/components/chat` 폴더 내의 `ChatModal.js`와 `ChatRoom.js` 컴포넌트**에서 구현되었습니다.

`Stomp.js`를 사용한 코드 흐름은 다음과 같습니다.
1.  **연결(Connection):** 사용자가 채팅 아이콘을 클릭하면, `Stomp.over(new SockJS(SERVER_URL))` 코드를 통해 SockJS 기반의 웹소켓 연결을 생성합니다. 그 후 `stompClient.connect(headers, onConnected, onError)` 메소드를 호출하여 서버에 연결을 시도합니다. 이때 `headers`에는 JWT 인증 토큰을 담아 보냅니다.
2.  **구독(Subscription):** `onConnected` 콜백 함수가 실행되면, 즉 연결이 성공하면, `stompClient.subscribe('/user/queue/private', onMessageReceived)` 코드를 통해 서버로부터 오는 1:1 메시지를 수신할 개인 큐를 구독합니다.
3.  **발행(Publishing):** 사용자가 채팅 입력창에 메시지를 입력하고 '전송' 버튼을 누르면, `stompClient.publish({ destination: '/app/private-chat/admin', body: message })`와 같은 코드가 실행됩니다. 이 메시지는 STOMP 브로커를 통해 서버의 `@MessageMapping`이 정의된 컨트롤러로 전달됩니다.
4.  **수신(Receiving):** 구독 중인 큐로 새로운 메시지가 들어오면 `onMessageReceived` 콜백 함수가 실행되고, 이 함수 안에서 Redux 액션을 디스패치하여 채팅 메시지 목록 상태를 업데이트하고 UI를 다시 렌더링합니다."

</p>
</details>

<details>
<summary>채팅 메시지나 관리자 페이지의 데이터를 Redux 스토어에서 관리하셨을 텐데, 실시간으로 들어오는 데이터를 Redux 상태와 어떻게 동기화했는지, 그리고 이때 발생할 수 있는 성능 문제에 대해 어떻게 고민하셨는지 궁금합니다.</summary>
<p>

**답변 예시:**
"네, 실시간 데이터는 Redux 스토어를 통해 관리했습니다. 웹소켓을 통해 새로운 메시지가 수신되면, `onMessageReceived` 콜백 함수에서 해당 메시지 데이터를 payload에 담아 Redux 액션(e.g., `chat/addMessage`)을 디스패치했습니다. 그러면 `chatSlice`의 리듀서가 이 액션을 받아 기존 메시지 배열(state)에 새로운 메시지를 추가하고, `useSelector`를 통해 이 상태를 구독하고 있던 채팅 컴포넌트가 자동으로 리렌더링되는 방식으로 동기화했습니다.

**성능 문제에 대한 고민:**
채팅 메시지가 매우 빠르게 수신될 경우, 매 메시지마다 액션을 디스패치하고 리렌더링하는 것이 성능에 부담을 줄 수 있다고 생각했습니다. 

이를 해결하기 위해 두 가지를 고민했습니다.
1.  **컴포넌트 최적화:** 메시지를 표시하는 `MessageItem` 컴포넌트를 `React.memo`로 감싸서, props가 변경되지 않은 메시지 아이템은 불필요하게 리렌더링되지 않도록 최적화했습니다.
2.  **메시지 버퍼링/배치 처리 (고민 단계):** 실제 구현은 못했지만, 만약 성능 문제가 심각했다면, 짧은 시간(e.g., 100ms) 동안 들어온 메시지를 배열에 모았다가 한 번에 하나의 액션으로 디스패치하는 '배치(batch) 처리'나 '디바운싱(debouncing)' 기법을 도입하는 것을 고려했을 것입니다. 이를 통해 Redux 상태 업데이트와 리렌더링 횟수를 줄여 성능을 개선할 수 있었을 것이라 생각합니다."

</p>
</details>

---

### **2. Team_project_full_stack (가상 의류 쇼핑몰)**

#### **2.1. JavaScript 및 상태 관리**

<details>
<summary>이 프로젝트의 핵심은 `localStorage.js` 모듈을 통해 서버 없이 상태를 관리한 것으로 보입니다. 이렇게 직접 클라이언트 사이드 '데이터베이스'를 구현하게 된 계기는 무엇인가요?</summary>
<p>

**답변 예시:**
"이 프로젝트는 저희가 HTML, CSS, JavaScript를 막 배운 뒤 진행한 첫 팀 프로젝트였습니다. 당시 저희의 주된 학습 목표는 백엔드나 프레임워크의 도움 없이, 순수 JavaScript만으로 웹 애플리케이션의 핵심 기능(회원가입, 로그인, 장바구니 등)을 구현해보는 것이었습니다.

`localStorage.js` 모듈을 직접 구현하게 된 것은, 서버의 역할을 클라이언트 사이드에서 흉내 내보자는 아이디어에서 시작되었습니다. 이를 통해 데이터가 어떻게 저장되고, 여러 페이지에서 어떻게 공유되며, 사용자의 액션에 따라 어떻게 변경되는지에 대한 전체적인 데이터 흐름을 깊이 있게 이해할 수 있었습니다. 프레임워크가 추상화해주는 상태 관리의 내부 동작 원리를 직접 구현해보는 값진 경험이었습니다."

</p>
</details>

<details>
<summary>`localStorage.js`의 `modifyNickname`과 같은 수정 함수를 보면, 전체 사용자 목록을 가져와서 특정 사용자를 찾은 뒤, 전체 목록을 다시 저장하는 방식으로 동작합니다. 데이터 양이 많아질 경우 이 방식의 잠재적인 성능 문제점은 무엇일까요? 만약 개선한다면 어떤 방식으로 접근하시겠습니까?</summary>
<p>

**답변 예시:**
"네, 정확히 보셨습니다. 해당 방식은 데이터가 적을 때는 문제가 없지만, 사용자 수가 수천, 수만 명으로 늘어날 경우 심각한 성능 저하를 유발할 수 있습니다.

**성능 문제점:**
1.  **느린 직렬화/역직렬화:** 데이터가 커질수록 `JSON.parse()`와 `JSON.stringify()`에 걸리는 시간이 길어져 UI를 멈추게 할 수 있습니다.
2.  **메모리 사용량 증가:** 전체 사용자 목록을 메모리에 한 번에 올려야 하므로 메모리 사용량이 급증합니다.
3.  **동기적 블로킹:** `localStorage` API는 동기적으로 동작하기 때문에, 데이터를 읽고 쓰는 동안 브라우저의 메인 스레드가 멈춰 다른 모든 사용자 인터랙션이 불가능해집니다.

**개선 방안:**
만약 개선한다면, `localStorage`를 거대한 JSON 덩어리로 사용하는 대신, **Key-Value 저장소**의 특성을 더 잘 활용하겠습니다. 예를 들어, 전체 사용자 목록 대신 각 사용자를 고유한 키(e.g., `user-mineruwo`)로 저장하는 것입니다. 

`localStorage.setItem('user-mineruwo', userObject);`

이렇게 하면 닉네임을 수정할 때, 전체 목록을 다룰 필요 없이 해당 사용자의 키 값만으로 데이터를 읽고 쓸 수 있습니다. 이렇게 하면 데이터의 크기와 상관없이 훨씬 빠르고 효율적으로 데이터를 수정할 수 있습니다."

</p>
</details>

<details>
<summary>`localStorage`는 문자열만 저장할 수 있는데, 객체나 배열 형태의 데이터를 저장하고 읽어오기 위해 어떤 함수(`JSON.stringify`, `JSON.parse`)를 사용하셨는지, 그리고 그 이유에 대해 설명해주세요.</summary>
<p>

**답변 예시:**
"네, `localStorage`는 Key-Value 형태로 데이터를 저장하지만, Value는 반드시 문자열(String) 타입이어야 합니다. 저희 프로젝트의 사용자 정보나 장바구니 목록은 여러 속성을 가진 객체(Object)나 배열(Array) 형태였기 때문에, 이를 문자열로 변환하는 과정이 필요했습니다.

-   **저장할 때:** `JSON.stringify()` 함수를 사용했습니다. 이 함수는 JavaScript 객체나 배열을 JSON 형식의 문자열로 변환(직렬화)해줍니다. 이 변환된 문자열을 `localStorage.setItem()`의 값으로 저장했습니다.
-   **읽어올 때:** `localStorage.getItem()`으로 읽어온 값은 JSON 형식의 문자열이므로, 이를 다시 JavaScript 객체나 배열로 사용하기 위해 `JSON.parse()` 함수를 사용했습니다. 이 함수는 JSON 문자열을 파싱하여 원래의 JavaScript 객체/배열로 변환(역직렬화)해줍니다.

이 두 함수를 통해, `localStorage`가 문자열만 저장할 수 있다는 제약에도 불구하고 복잡한 데이터 구조를 효과적으로 저장하고 관리할 수 있었습니다."

</p>
</details>

#### **2.2. DOM 조작 및 MPA 구조**

<details>
<summary>`p_myPage` 폴더를 보면 `modify.html`, `orderList.html` 등 여러 HTML 파일로 페이지가 나뉘어 있습니다. 이렇게 MPA(Multi-Page Application) 구조에서 페이지 이동 시 상태(e.g., 로그인 정보)를 유지하기 위해 어떤 방법을 사용하셨나요? (`localStorage.js`의 `currentLoginInfo` 함수와 관련지어 설명해주세요.)</summary>
<p>

**답변 예시:**
"네, 이 프로젝트는 각 페이지가 별도의 HTML 파일로 구성된 MPA(Multi-Page Application) 구조입니다. 페이지가 새로고침될 때마다 JavaScript 컨텍스트가 초기화되기 때문에, 페이지 간 상태 유지를 위해 **`localStorage`를 중앙 저장소처럼 활용**했습니다.

예를 들어, 로그인 페이지에서 로그인이 성공하면, `localStorage.js`의 `loginUser` 함수가 호출되어 `localStorage`의 'currentLogin'이라는 키에 현재 로그인한 사용자 정보를 JSON 문자열 형태로 저장합니다.

그 후, 사용자가 마이페이지(`myPage.html`)로 이동하면, 해당 페이지에 포함된 `myPageJS.js` 스크립트가 실행되면서 가장 먼저 `localStorage.js`의 `currentLoginInfo()` 함수를 호출합니다. 이 함수는 `localStorage`에서 'currentLogin' 키의 값을 읽어와 사용자 객체로 파싱하여 반환합니다. 만약 반환된 값이 없다면(로그인하지 않은 상태), 로그인 페이지로 리디렉션시키는 로직을 구현하여 인증 상태를 유지했습니다."

</p>
</details>

<details>
<summary>`myPageJS.js`나 `modifyInfoJS.js`와 같은 파일에서 `localStorage`로부터 읽어온 데이터를 화면에 표시하기 위해 어떤 DOM API를 주로 사용하셨나요? (e.g., `document.getElementById`, `innerHTML`, `createElement` 등)</summary>
<p>

**답변 예시:**
"주로 바닐라 JavaScript의 기본 DOM API를 사용했습니다. 

데이터를 화면에 표시할 때는, 먼저 `document.getElementById()`나 `document.querySelector()`를 사용해 데이터를 표시할 HTML 요소를 선택했습니다. 그 다음, 해당 요소의 `innerHTML`이나 `textContent` 속성을 `localStorage`에서 가져온 데이터로 변경하는 방식을 사용했습니다.

예를 들어, `myPageJS.js`에서는 `currentLoginInfo()`로 가져온 사용자 객체의 `name` 속성을 `document.getElementById('username').textContent = userInfo.name;`과 같은 코드로 화면에 표시했습니다.

동적으로 목록(e.g., 주문 목록)을 만들어야 할 때는 `document.createElement('li')`로 새로운 HTML 요소를 생성하고, `appendChild()` 메소드를 사용해 부모 요소에 추가하는 방식으로 UI를 구성했습니다."

</p>
</details>

<details>
<summary>프레임워크 없이 순수 JavaScript로만 개발하면서 가장 어려웠던 점은 무엇이었나요? 특히 '컴포넌트' 개념의 부재와 상태 변경에 따른 UI 업데이트를 수동으로 처리하는 과정의 어려움에 대해 말씀해주세요.</summary>
<p>

**답변 예시:**
"가장 어려웠던 점은 말씀하신 대로 **상태와 UI의 동기화를 수동으로 관리**하는 것이었습니다.

React와 같은 프레임워크는 상태가 변경되면 알아서 UI를 다시 렌더링해주지만, 저희는 모든 것을 직접 처리해야 했습니다. 예를 들어, 사용자가 닉네임을 변경하면, `localStorage`의 데이터를 업데이트하는 것뿐만 아니라, 헤더에 있는 닉네임, 마이페이지에 있는 닉네임 등 화면에 표시된 모든 닉네임을 수동으로 찾아 `textContent`를 바꿔주는 코드를 일일이 작성해야 했습니다. 이 과정에서 하나라도 놓치면 데이터와 UI가 일치하지 않는 버그가 발생했습니다.

또한, **'컴포넌트' 개념의 부재**도 어려움이었습니다. 헤더나 푸터처럼 여러 페이지에서 반복적으로 사용되는 UI 요소들도 각 HTML 파일에 중복해서 존재했습니다. 이 때문에 작은 수정 사항 하나가 생겨도 관련된 모든 HTML 파일을 찾아 동일한 내용을 수정해야 하는 비효율적인 작업을 반복해야 했습니다.

이 프로젝트를 통해 프레임워크가 왜 필요한지, 특히 선언적 UI와 컴포넌트 기반 아키텍처가 개발 생산성과 유지보수성을 얼마나 크게 향상시키는지 몸소 깨닫게 되었습니다."

</p>
</details>
