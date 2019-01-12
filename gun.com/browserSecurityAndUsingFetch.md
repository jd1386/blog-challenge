cdn - jquery, underscore의 cdn을 이용해서 js파일을 갖다쓸 수 있음

### http

- stateless하다

- connectionless하다

- method

  - GET - server에 자원을 요청 하는 것
  - POST-server에 자원을 생성 하는 것
  - DELETE- server에 자원을 제거하는 것
  - PUT-server에 자원을 수정하는 것

  script tag와 같은 것들로 공격받지 않기위해 cors에러를 띄워줌

  OPTION 메소드는 미리 보내서 cors에러가 있는지 확인을 함

  - 간단한 요청과 다르게, "preflighted"(사전 전달) 요청은 먼저, 실제 요청이 전송하기에 안전한지 아닌지를 결정하기 위해, 다른 도메인에 있는 리소스에 `OPTIONS` 메서드로 HTTP 요청을 전송합니다. Cross-site 요청은 사용자 데이터에 대한 함축적인 의미를 가지고 있기에 이와 같이 사전 전달됩니다. 특히, 다음과 같은 경우에 요청이 사전 전달됩니다(참고: https://developer.mozilla.org/ko/docs/Web/HTTP/Access_control_CORS)

### fetch

server에 POST하는 방법

```javascript
fetch('http://52.78.213.9:3000/messages', {
  method : 'POST',
    body : JSON.stringify(messages),
    headers : {
      'Content-Type' : 'application/json'
    }
  }).then(res => res.json())
  .then(response => console.log('Success : ', JSON.stringify(response)))
  .catch(error => console.log(error);
```

server에서 GET하는 방법

```javascript
let server = 'http://52.78.213.9:3000/messages';
fetch(server, {
    mathod : 'GET',
    headers : {
      "Content-type" : "application/json"
    },
    mode : 'cors',
    cache : 'default'
  })
  .then(response => {
    return response.json();
}).then(json => {
    return json;
}
```

이번 sprint를 하면서 새로 알게된 지식: 어떤 노드에 자식노드를 넣어주는데 상위에서 업데이트 되게하려면 appendChild를 하지않고 prepend()를 하면된다!

#### fetch는 ajax 방법중 하나인가?

Ajax는 클라이언트에서 서버측에 '비동기'로 요청(get, post, put 등)하여 서버와 interact 하는 방식 또는 기술을 통칭하고 fetch란 Ajax 기술 (좀 더 정확히는 XMLHttpRequest)을 Promsie 객체 등을 사용하여 좀 더 편리하게 이용할 수 있게 하는 비동기 요청 API이다.

웹 API로서 fetch를 사용하는데 주의해야 할 점은 인터넷 익스플로러는 지원하지 않는다는 점이다. (<https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API>) 따라서 jQuery의 ajax 메서드를 이용하거나 axios 등의 모듈을 사용하는 것이 일반적이며 XMLHttpRequest를 직접 이용하는 것도 가능하나 불편한 점이 많아서 실제로 사용되는 경우는 드물다.



 