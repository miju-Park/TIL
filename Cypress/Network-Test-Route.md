# Cypress에서 API 테스트 방법
| 참고 사이트 : https://www.valentinog.com/blog/fake/

## Fake API가 필요한 이유

FE개발을 할 때, 개발한 코드 검증을 위해 API 서버와 dependency를 분리하는게 좋다.
또한, API 호출에 비용이 들거나 방화벽 문제로 외부 접속이 막혀 있는 경우, API 응답이 느린 상황 등에서 API 서버와 분리된 환경에서 개발하는 상황이 필요하다.
이 때, mocking과 stubbing을 사용하게 된다.

## mock, stub 차이점

둘 다 개발과 테스트시 test double(가짜 데이터)를 사용하는 개념은 동일하다.

### Mock

* 함수를 가짜 데이터로 교체하는 방법
* 테스트에서 외부로 나가는 의존성(outgoing dependencies)를 교체하는 방법
* Fetch / XMLHttpRequest를 테스트용 버전으로 교체하는 방법

### Stub

* stub : 외부 서비스, 네트워크 응답을 가짜 데이터 버젼으로 교체하는 방법
* 외부에서 들어오는 의존성(incoming dependencies)를 교체하는 방법
* Fetch / XMLHttpRequest 응답을 가로채는 방법

## Cypress에서 Stub 사용하여 테스트하기

cypress에서 기본적으로, **XMLHttpRequest** response를 응답할 수 있고, 설정을 추가하면 **fetch** 응답도 사용할 수 있다.

cypress.json 파일에 아래 내용을 추가하면 된다.

```javascript
{
  "experimentalFetchPolyfill": true
}
```

테스트 대상 프로젝트에서 **/api/users/** API를 호출한다고 가정했을 때, 

```javascript
  it("should see a list of users", () => {
    cy.visit("/");

    cy.server();
    cy.route({
      url: "/api/users/",
      method: "GET",
      response: [
        {
          name: "Juliana",
          surname: "Crain"
        },
        { name: "Molly", surname: "F." }
      ]
    });
    //test script..
  });
});
```

위와 같이 테스트 코드를 작성하면, /api/users의 API 응답을 지정한 response로 교체하여 어플리케이션으로 전달하게 된다.
(! 이 때, API 응답이 없는 경우 - 404 Not Found는 실행되지 않음.)

또한, 테스트 상황에 따라 API 응답을 다르게 지정할 때, fixture를 사용하여 response 값을 정의해두고 아래와 같이 사용하면 편리하다.

```javascript
cy.route({'/api/users','fixtures:users.json'})
```





