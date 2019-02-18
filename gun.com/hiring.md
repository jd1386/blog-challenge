## hiring assessment 정리

#### module.exports와 exports의 차이

----------------------------------------------------------------------------------------------------------------

```java	
//exports 의 예시 exports object의 property로 활용하는 것
exports.area = (width) => width * width;
exports.perimeter = (width) => 4 * width;
// exports의 예시 한번에 export 한다.
module.exports = {
  area: (width) => width * width,
  perimeter: (width) => 4 * width
}
// 사용할 때
// exports
const expo = require('./sample.js')
    expo.area blahblah
// module.exports
const expo = require('./sample.js')
expo.area blah
```



### SQL과 NOSQL의 차이

---

1. SQL

   안전한 것이 장점이고 데이타가 많을수록 장점이 많다. 하지만 고정적이어서 혹시나 데이터를 옮겨야할 때 

   힘들다는 것이 단점이다.

2. NOSQL 

   처음에 특정한 틀없이도 바로 document를 만들어낼 수 있다. 구조화되어있지 않아서 다이나믹하고 유연하다.

   각각의 document가 유니크한 구조를 가진다.

SQL은 수직적으로 NOSQL은 수평적으로 데이터를 늘려나간다. NOSQL이 더 많은 traffic을 사용한다.

이는 한건물에 위로 층수가 높아지는 것과 여러 건물이 생기는 것과 비슷하다.

#### 그렇다면 언제 어떤 DB를 써야하는가?

1.  먼저 SQL은 프로젝트가 미리 규정하고 틀을 잡아야 하는 경우 쓰면 좋다. 예로 계산 시스템이나 모니터 인벤토리 시스템과 같이 multi-row transactions가 필요한 경우. 또는 legacy system 즉 예전의 것들을 같이 사용하는 시스템에서도 많이 쓰인다.
2. NOSQL은 명확한 틀이 없고 빠른 성장이 있을 프로젝트에 많이 쓰인다. 데이터베이스에 스키마를 규정할 수 없다면 혹은 스키마가 계쏙 변한다면 써야한다.



- 공부하면서 알게된 사실 : 일반 HTTP요청에서 server는 응답을 넘겨줄 때 res.end(data)에만 담아도 res.body에 

  data를 넘겨줄 수 있다.

###  inheritance pattern (functional, shared, prototypal, pseudoclassical)

- functional: someinstance 라는 object가 있고 property로 여러 function들을 갖는다. 마지막엔 someinstance를 리턴한다. 모든 것이 class 안에 들어간다.

- functional-shared: class와 classMethod를 구분해서 정의한 후 extend라는 function을 정의해서 class 안의 someinstance와 classMethod를 extend한다.

- prototypal: class와 classMethod를 따로 정의하고 class 안에서 Object.create를 이용하여 someInstance를 classMethod로 복사한 후 리턴한다.(필요한 값이 있는 경우 복사 후 넣어준다. 밑에 예시)

  ```java	
  const someInstance = Object.create(queueMethods);
    someInstance.value = value;
  ```

- pseudoclassical: class에는 기본적인 값만 넣어주고 나머진 전부 prototype에 넣는방식.

