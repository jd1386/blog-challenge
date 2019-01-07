```javascript
var x = 10;
function f () {
  x = x + 1;
  return x;
}

function add (x, y) { return x + y; }

var result = add(x, f());
```

위와 같은 경우 add(x,f()) 실행될 때 x값이 바로 들어감.

### checkpoint 9

primitive type -> stack area에 저장됨

reference type -> heap area에 저장되고 참조함

참조 재할당을 주의하면서 object를 바라봐야함

```javascript
var myArray = [2, 3, 4, 5];
function doStuff(arr) {
  arr = [ ];
}
doStuff(myArray);
```

myArray는 [2,3,4,5]를 참조하고 arr은 []를 참조하므로 myArray는 그대로