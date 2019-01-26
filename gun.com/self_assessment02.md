time complexity를 구하는 문제에서 두가지 궁금했던 점이 있었다.

```javascript
var bruteForcePassword = function(max) {
  var alphabet = 'abcdefghijklmnopqrstuvwxyz';

  var findPassword = function(attempt) {
    if (attempt.length > 0) {
      console.log('Trying ' + attempt);
    }
    if (attempt.length <= max) {
      for (var i = 0; i < alphabet.length; i++) {
        findPassword(attempt.concat(alphabet[i]));
      }
    }
  };

  findPassword('');
};

```
위와 같은 코드였는데, 궁금했던 점은 위의 패스워드를 찾는 방식이 complexity를 생각할 
것도 없이 패스워드를 찾을 수 없다고 생각했는데, 코드를 잘 들여다보면 첫번째의 letter에 
'a'부터 'z'까지 오고 다음 letter에도 'a' 부터 'z' 까지 오고 그게 max까지 쭉 채워지므로 모든 경우의 수를 다생각 할 수 있다. 따라서 complexity가 exponential 이 된다.

다음의 문제는 
```javascript
var makeRange = function(array) {
  array.forEach(function(item) {
    for (var i = 1; i < 10; i++) {
      console.log(item + i);
    }
  });
};

```
위의 코드의 complexity였는데 n이 작을 때는 n^2이라고 생각할 수 있지만 n이 커지면 커질수록 9n은 n^2보다는 n에 가까우므로 complexity는 n이 된다.
