 ## 1. HTML / CSS 기본

  ### 1-1. 시맨틱 태그 (Semantic Tags)

     핵심 개념:*
      *   시맨틱 태그는 <div>, <span>처럼 의미 없이 영역만 나누는 태그와 달리, <header>, <nav>, <main>, <footer>처럼
  태그 자체가 콘텐츠의 의미와 구조를 설명해주는 태그를 말합니다.
         사용 이유:*
          1.  SEO (검색 엔진 최적화): 검색 엔진이 웹페이지의 구조를 더 잘 이해하고 중요한 콘텐츠를 파악하는 데 도움을
  줍니다.
          2.  웹 접근성 향상: 스크린 리더와 같은 보조 기기가 페이지 구조를 쉽게 파악하여 시각 장애인 사용자에게 더 나은
  경험을 제공합니다.
          3.  코드 가독성 및 유지보수: 개발자가 태그만 보고도 코드의 구조를 쉽게 파악할 수 있습니다.

     ✅ 간단한 실습/과제:*
      *   <div> 태그만으로 웹페이지 레이아웃을 만드는 것과, 시맨틱 태그를 사용하는 것의 차이점을 SEO와 웹 접근성
  관점에서 설명해보세요.

     ➡️ 예시 답변 및 풀이:*
      <div>만 사용하면 모든 영역이 구조적으로 동일한 중요도를 갖는 것으로 인식됩니다. 하지만 <header>, <main>, <footer>
  같은 시맨틱 태그를 사용하면, 검색 엔진은 <main> 내부의 콘텐츠가 페이지의 핵심 내용임을 명확히 알 수 있어 SEO에
  유리합니다. 또한, 스크린 리더 사용자는 "메인 콘텐츠로 바로 가기"와 같은 기능을 통해 원하는 정보에 빠르게 접근할 수
  있어 웹 접근성이 크게 향상됩니다.

  ---

  ## 2. JavaScript Core

  ### 2-1. var, let, const의 차이와 호이스팅

     핵심 개념:*
         스코프(Scope):* 변수가 유효한 범위.
          *   var: 함수 스코프(function-scoped).
          *   let, const: 블록 스코프(block-scoped, {} 기준).
         재할당/재선언:*
          *   var: 재선언, 재할당 모두 가능.
          *   let: 재할당은 가능, 재선언은 불가능.
          *   const: 재선언, 재할당 모두 불가능. (단, 객체나 배열의 내부 값은 변경 가능)
         호이스팅(Hoisting):* 코드가 실행되기 전, 변수와 함수 선언이 해당 스코프의 최상단으로 끌어올려지는 현상.
          *   var: 선언부가 호이스팅되며 undefined로 초기화됩니다. 선언 전에 접근해도 에러가 나지 않습니다.
             `let`, `const`: 선언부만 호이스팅되며, 초기화되지 않습니다. 이 때문에 선언 전에 접근하면 TDZ(Temporal Dead 
  Zone)*에 빠져 참조 에러(ReferenceError)가 발생합니다.

     ✅ 간단한 실습/과제:*
      *   TDZ(Temporal Dead Zone)가 무엇인지, 그리고 let과 const가 var와 달리 TDZ의 영향을 받는 이유를 설명해보세요.

     ➡️ 예시 답변 및 풀이:*
      TDZ는 '일시적 사각지대'로, 스코프에 진입한 시점부터 변수 선언문에 도달하기까지의 구간을 의미합니다. var는
  호이스팅될 때 undefined로 초기화되어 이 구간이 사실상 없지만, let과 const는 호이스팅 시 초기화되지 않기 때문에 TDZ가
  존재합니다. 이 구간에서 해당 변수에 접근하려고 하면, 변수는 이미 존재하지만 아직 초기화되지 않았다는 참조 에러가
  발생합니다. 이는 var의 비직관적인 동작을 막고 코드의 안정성을 높이기 위해 도입된 메커니즘입니다.

  ### 2-2. Promise와 async/await

     핵심 개념:*
         Promise:* 비동기 작업의 최종 성공 또는 실패를 나타내는 객체. .then()으로 성공 시, .catch()로 실패 시의 로직을
  체이닝하여 콜백 지옥을 해결합니다.
         async/await:* Promise를 동기 코드처럼 보이게 만들어 가독성을 높이는 문법. async 함수 내에서 await 키워드를
  사용하여 Promise가 처리될 때까지 기다립니다. 에러 처리는 try...catch 구문을 사용합니다.

     ✅ 간단한 실습/과제:*
      *   setTimeout을 사용하여 1초 뒤에 "완료!"를 출력하는 Promise를 만들고, 이를 async/await 구문으로 호출하는 코드를
  작성해보세요.

     ➡️ 예시 답변 및 풀이:*
      `javascript
      // 1. 1초 뒤에 성공하는 Promise 생성
      function delay(ms) {
        return new Promise(resolve => {
          setTimeout(() => {
            resolve("완료!");
          }, ms);
        });
      }


      // 2. async/await를 사용하여 Promise 호출
      async function runAsync() {
        try {
          console.log("작업 시작...");
          const result = await delay(1000); // 1초를 기다림
          console.log(result); // "완료!" 출력
        } catch (error) {
          console.error(error);
        }
      }

      runAsync();

  `
      async/await를 사용하면 delay(1000)이라는 비동기 코드가 마치 동기 코드처럼 순차적으로 실행되는 것처럼 보여 가독성이
  매우 좋아집니다.

  ---

  ## 3. React 핵심 개념

  ### 3-1. 가상 DOM (Virtual DOM)

     핵심 개념:*
      *   실제 DOM의 구조를 흉내 내는 간단한 JavaScript 객체. 메모리에 존재하여 조작 비용이 저렴합니다.
         동작 방식 (재조정, Reconciliation):*
          1.  상태(state)가 변경되면, React는 새로운 가상 DOM 트리를 생성합니다.
          2.  이전 가상 DOM 트리와 새로운 가상 DOM 트리를 비교하여 변경된 부분만 찾아냅니다 (이 과정을 Diffing이라고
  합니다).
          3.  변경이 필요한 부분만 모아서 한 번에 실제 DOM에 적용합니다 (이를 Batch Update라고 합니다). 이를 통해
  불필요한 DOM 조작을 최소화하여 성능을 향상시킵니다.

     ✅ 간단한 실습/과제:*
      *   React가 실제 DOM을 직접 조작하지 않고 가상 DOM을 사용하는 이유를 '성능' 관점에서 설명해보세요.

     ➡️ 예시 답변 및 풀이:*
      실제 DOM 조작은 브라우저의 렌더링 엔진을 직접 건드리는 비싼 작업입니다. 작은 변화 하나에도 전체 레이아웃을 다시
  계산(Reflow)하고 다시 그리는(Repaint) 과정이 발생할 수 있어 성능 저하의 주된 원인이 됩니다. React는 이러한 변경사항들을
   메모리상의 가상 DOM에서 미리 계산하고, 최종적인 변경사항만 묶어서 실제 DOM에 딱 한 번 적용합니다. 이는 마치 여러
  가구를 옮길 때 하나씩 옮기는 대신, 최종 배치도를 그린 후 한 번에 옮기는 것과 같아 훨씬 효율적입니다.

  ### 3-2. 클래스 컴포넌트 vs 함수형 컴포넌트와 Hooks

     핵심 개념:*
         Hooks (`useState`, `useEffect` 등):* 함수형 컴포넌트에서도 상태 관리나 생명주기 관리 등 클래스 컴포넌트의 기능을
   사용할 수 있게 해주는 기능입니다.
         등장 배경:* 클래스 컴포넌트의 복잡성(this 바인딩), 로직 재사용의 어려움(HOC, Render Props 패턴), 비대해지는
  생명주기 메서드 등의 문제를 해결하기 위해 등장했습니다.

     ✅ 간단한 실습/과제:*
      *   useState와 useEffect를 사용하여, 버튼을 누르면 숫자가 1씩 증가하고, 숫자가 변경될 때마다 웹 브라우저의 타이틀이
   '현재 숫자: [숫자]'로 바뀌는 카운터 컴포넌트를 만들어보세요.

     ➡️ 예시 답변 및 풀이:*
      `jsx
      import React, { useState, useEffect } from 'react';

      function Counter() {
        // useState: count라는 상태와, 이 상태를 변경할 setCount 함수를 생성
        const [count, setCount] = useState(0);


        // useEffect: count 상태가 변경될 때마다 실행될 부수 효과(side effect)를 정의
        useEffect(() => {
          // 브라우저의 타이틀을 변경
          document.title = 현재 숫자: ${count};
        }, [count]); // 의존성 배열에 count를 넣어, count가 변경될 때만 이 effect가 실행되도록 함


        return (
          <div>
            <p>현재 숫자: {count}</p>
            <button onClick={() => setCount(count + 1)}>증가</button>
          </div>
        );
      }

  `

  ### 3-3. React 생명주기 (useEffect 중심)

     핵심 개념:*
      *   useEffect(callback, [dependencies])는 두 번째 인자인 의존성 배열에 따라 실행 시점이 달라집니다.
             `[]` (빈 배열): 컴포넌트가 처음 렌더링(마운트)될 때 한 번만* 실행됩니다. (API 최초 호출 등)
          *   [someValue]: 맨 처음 렌더링될 때, 그리고 의존성 배열 안의 someValue가 변경될 때마다 실행됩니다.
          *   생략: 컴포넌트가 리렌더링될 때마다 실행됩니다. (주의해서 사용해야 함)

     ✅ 간단한 실습/과제:*
      *   React 컴포넌트가 처음 렌더링될 때만 API를 호출하여 데이터를 가져오고 싶다면, useEffect를 어떻게 작성해야
  하는지 설명하세요.

     ➡️ 예시 답변 및 풀이:*
      useEffect의 두 번째 인자로 빈 배열([])을 전달해야 합니다.
      `jsx
      useEffect(() => {
        // 이 부분은 컴포넌트가 처음 렌더링될 때 단 한 번만 실행됩니다.
        fetchData(); // API를 호출하는 함수
      }, []);

  `
      이렇게 하면 불필요한 리렌더링 시마다 API가 반복적으로 호출되는 것을 막아 성능을 최적화하고 서버 부하를 줄일 수
  있습니다.

  ---

  ## 4. API 통신 (Axios)

  ### 4-1. 클라이언트-서버 통신

     핵심 개념:*
      *   프론트엔드(클라이언트)는 사용자의 인터랙션에 따라 필요한 데이터를 백엔드(서버)에 요청하고, 서버는 요청에 맞는
  데이터를 응답으로 보내줍니다.
      *   Axios는 Promise 기반의 HTTP 통신 라이브러리로, fetch에 비해 사용법이 간편하고 다양한 편의 기능을 제공합니다.

     ✅ 간단한 실습/과제:*
      *   React 컴포넌트가 마운트될 때, axios를 사용하여 외부 API(https://jsonplaceholder.typicode.com/users/1)에서
  사용자 데이터를 가져와 화면에 이름을 표시하는 코드를 작성해보세요.

     ➡️ 예시 답변 및 풀이:*
      `jsx
      import React, { useState, useEffect } from 'react';
      import axios from 'axios';


      function UserProfile() {
        const [user, setUser] = useState(null);
        const [loading, setLoading] = useState(true);


        useEffect(() => {
          const fetchUser = async () => {
            try {
              const response = await axios.get('https://jsonplaceholder.typicode.com/users/1');
              setUser(response.data); // 데이터 상태 업데이트
            } catch (error) {
              console.error("데이터를 불러오는 데 실패했습니다.", error);
            } finally {
              setLoading(false); // 로딩 상태 종료
            }
          };


          fetchUser();
        }, []); // 빈 배열로 마운트 시 한 번만 실행

        if (loading) {
          return <div>로딩 중...</div>;
        }


        return (
          <div>
            <h1>사용자 정보</h1>
            {user && <p>이름: {user.name}</p>}
          </div>
        );
      }

  `

  ---

  ## 5. 브라우저 저장소

  ### 5-1. localStorage vs sessionStorage vs Cookie

     핵심 개념:*
      *   웹 브라우저에서 데이터를 저장하기 위한 세 가지 주요 기술. 각각의 특징과 용도가 다릅니다.

     ✅ 간단한 실습/과제:*
      *   localStorage, sessionStorage, Cookie의 차이점을 데이터 생명주기, 저장 용량, 서버 전송 여부 관점에서 비교
  설명하세요.

     ➡️ 예시 답변 및 풀이:*

  | 특징 | localStorage | sessionStorage | Cookie |
  | --- | --- | --- | --- |
  | 생명주기 | 영구적 (사용자가 직접 삭제하기 전까지 유지) | 세션 단위 (브라우저 탭/창을 닫으면 소멸) | 설정된 만료일까지
   유지 |
  | 저장 용량 | 큼 (약 5MB) | 큼 (약 5MB) | 작음 (약 4KB) |
  | 서버 전송 | 전송 안 됨 (클라이언트에만 저장) | 전송 안 됨 (클라이언트에만 저장) | 모든 HTTP 요청에 자동으로 포함되어
  서버로 전송됨 |
  | 주 사용처 | 자동 로그인, UI 테마 설정 등 | 일회성 정보 (입력 폼 데이터 등) | 서버가 클라이언트를 식별하기 위한 인증
  상태 유지 |