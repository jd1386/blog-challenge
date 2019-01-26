- this- this는 호출이 중요 해당부분이 괄호없이 호출이 안되면 의미가 없음

  ```javascript
  var name = "Window";
  var alice = {
    name: "Alice",
    sayHi: function() {
      alert(this.name + " says hi");
    }
  };
  var bob = { name: "Bob" };
  setTimeout(alice.sayHi, 1000);
  ```

  이와 같은 경우에서도 익명의 function이 setTimeout이 들어가기 때문에 this === window 이다.

- setTimeout의 연기 시간이 0이어도 비동기로 뒤에 명령문들을 먼저 실행한다.

  ```javascript
  function foo () {
    var data = 10;
  
    bar(function (players) {
      data = players;
    });
  
    return data;
  }
  
  function bar (callback) {
    setTimeout(callback, 0);
  }
  
  var result = foo();
  ```

  이 경우에도 return data가 bar보다 먼저 실행된다.

  ### setTimeout에서의 this(immersive dancer-party의 keypoint)

  setTimeout에서의 첫번째 parameter의 this는 처음에는 우리가 의도한 this인 

  object를 가리키지만 두번째 호출될때부터는 window를 가리키게 된다.

  그래서 우리가 의도한대로 this를 바인딩시켜주려면 다음과 같이 해주면 된다.

  setTimeout(this.func.bind(this), wait)

