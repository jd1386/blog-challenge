# value & Reference

- 왜그런진 모르겠지만 다음과 같은 경우 myArray가 바뀌지 않는다.

  ```javascript
  var myArray = [2,3,4,5]
  var ourArray = myArray;
  ourArray = [];
  myArray?? 답은 [2,3,4,5]
  ```
