today i learn

package.json 파일 안에 'script' 항목은 어떤 커맨드를 입력했을 때 나오는 명령어들이다.

예를 들어 'start':'node basic-server.js' 라는 property가 'script'안에 있으면 

yarn start를 입력할 경우 위의 코드가 실행되어 node로 basic-server.js를 실행시킨다.



'husky'안에 hook은 pre-commit이라는 항목이 있는 경우가 있는데 이 경우는 커밋하기전에 코드를 es-lint로 확인한다던지 test를 돌려주는 명령들을 실행한다. 이 항목이 다른 역할을 수행하는 경우도 있는데, 만약 이미지 파일이 들어간다면 이 항목이 이미지파일을 파일에 맞게 최적화시켜주는 기능도 구현할 수가 있다.

'devDependencies'  이 항목에는 설치되어 있는 모듈들이 나온다.



npm --save옵션: 만약 현재 경로에 package.json이 존재하면 dependencies에 자동으로 포함된다.

npm --save-dev 옵션: 현재 경로에 package.json이 존재하면 devDependencies 항목에 자동으로 포함된다.



npm install 할때 -g or --global를 붙여주면 global에 install을 의미한다.

npm install  < folder > 다음과 같이 실행할 수도 있다. 

- `-P, --save-prod`: Package will appear in your `dependencies`. This is the default unless `-D` or `-O` are present.
- `-D, --save-dev`: Package will appear in your `devDependencies`.
- `-O, --save-optional`: Package will appear in your `optionalDependencies`.
- `--no-save`: Prevents saving to `dependencies`

https://docs.npmjs.com/cli/install 이 링크를 참고하면 npm install에 대해 알 수 있다.



#### what is stub?

stub은 조절가능한 대체재다 stub을 사용하면 코드를 테스트해 볼 수 있다. 코드에 대해 독립적으로 어떠한 교류없이.

#### what is api endpoint?

커뮤니케이션 채녈의 하나다.서버의 url로 나타나기도 한다. 

예로 OAuth는 세가지 endpoint가 있다. 필요할것으로 예상되는.

1. Temporary Credential Request URI (called the Request Token URL in the OAuth 1.0a community spec). This is a URI that you send a request to in order to obtain an unauthorized Request Token from the server / service provider.
2. Resource Owner Authorization URI (called the User Authorization URL in the OAuth 1.0a community spec). This is a URI that you direct the user to to authorize a Request Token obtained from the Temporary Credential Request URI.
3. Token Request URI (called the Access Token URL in the OAuth 1.0a community spec). This is a URI that you send a request to in order to exchange an authorized Request Token for an Access Token which can then be used to obtain access to a Protected Resource.





"`Access-Control-Allow-Origin: *`"는 서버에 리소스가 cross-site 방식 내에서 **모든** 도메인으로부터 접근 가능하다는 것을 의미한다.

Access-Control-Allow-Origin: http://foo.example는 다음의 것만 허용하는 것이다.(cors로)



nodemon을 쓰면 서버가 변경내용이 있을 때마다 서버를 새로 켜기 때문에 nodemon으로 키면 안된다.



lsof -i tcp:3000 이 명령어는 꺼지지않은 서버들을 확인해주는 명령어이고,kill -9 PID는 PID에 해당하는 연결을 끊어주는 명령어이다.

 커밋을 꼭하자! 하다가 안되면 다시 돌아갈 곳이 있어야 한다.



request 나 response나 둘다 header와 body가 있는데 header는 기준을 잡아주는 부분이고 body가 실제 내용이 담긴부분이다. 그리고 실제로 정보가 왔다갔다할때는 string이 binary로 전환되어 buffer의 도움을 받아 정보가 이동한다.

OPTIONS를 처리해주는 건 그냥 받아주기만 하면됌.

pkill node 끊어주는 걸 이것만 하면 바로 끊을 수 있음.

request가 한번에 오는게 아니기 때문에 on 이라는 비동기함수로 처리를 한다.

exports 보다 module.exports가 우선순위가 높음

다른파일에서 exports를 해서 함수를 실행해도 원래함수의 값을 바꿔준다.

동기가 다 비워져야 비동기가 실행됨.



common JS -> module exports와 같은 것들을 쓰는 총체적인 것들

서버가 하는일 CRUD 













