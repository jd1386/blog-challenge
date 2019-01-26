# Prototype

다른 언어에서의 class를 구현하기 위해서 존재하는 개념인데, 예를 들어 People이라는 다른 언어에서 말하는 class가 

존재한다면 이를 통해 person1, person2를 만든다고 가정해보자.

그렇다면 person1,2에 브라우저에서 제공하는 __ proto__ 라는  property 존재하게 된다.(사실상 JavaScript의 모든 

object에 __ proto__가 존재한다.)

이때의 __ proto__는 People을 가리키는 것이 아니라 People의 prototype이라는 property를 가리킨다.

또한 People의 prototype의 constructor는 다시 함수 People을 가리키게 된다.

이를 통해 Prototype의 장점을 알 수 있는데, 예를 들어 People이란 함수에 Fullname이라는 함수가 있다고 하면

person1, 2를 만들때마다 그 object에 Fullname이 들어가서 메모리의 사용량이 많아지겠지만, prototype에 

Fullname을 담아둔다면 object를 만들어낸 후 만들어진 person1,2와 같은 object들이 Person의 prototype의

Fullname을 가져와 쓰기때문에 메모리의 사용량이 줄어든다. 

Array.isArray는 내장된 함수

arr.map 은 prototype에 있는 메소드

new Array(4)  -> [empty*4]

extending prototype ex) Number.prototype에 메소드를 추가 시키는 것 조심해야함

call: 명시적으로 this 바인딩하는것

__ proto__ 는 read only

arrow function 은 prototype, constructor 안생김

### 상속방법 (매우 중요!!)

```javascript
function People(name){
    this.name = name;
}
People.prototype.introtuce = function(){
    console.log(`my name is ${this.name}`);
}
function Student(name, ...args){
    People.apply(this, args) //call도 가능(인자하나하나로 받을때)
}
Student.prototype = Object.create(People.prototype)
Student.prototype.constructor = Student;

```

위의 상속 과정에서 apply는 People안에 있는 것들을 상속받고, 

Object.create로는 prototype에 있는 것들을 담아준다.

그리고 constructor를 다시 원래 class로 지정을 해준다.

ES6 문법인 **class**를 사용하면 다음과 같다.

```javascript
class People{
    constructor(name){
    this.name = name;
    }

    introduce(){
        console.log(`my name is ${this.name}`
    }
}
class Student extends People{
    constructor(name, ...args){
    	super(name, args)
    }
    introduce(){
        super.introduce()
    }
}
```

위와 같이 상속하고 constructor밖이  pseudo-classical 방식의 prototype method를 

정의해주는 부분이라고 생각하면 편할 것이다.

혹시나 this.age = age와 같은 부분을 쓴다면 constructor안에 써줘야 할 것이다.