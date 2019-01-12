이번 스프린트의 keypoint는 크게 두가지 정도로 뽑을 수 있다.
첫번째로는 부모의 state를 자식에서 바꾸고 싶을 경우인데 그럴 경우엔 부모에 state를 바꾸는 함수를 지정한 후에 그 함수를 props로 넘겨주면 된다.
이를 코드로 옮기면 밑에와 같다.
```javascript
class Parent extends React.Component {
  constructor(props) {
    super(props)

    this.handler = this.handler.bind(this)
  }

  handler() {
    this.setState({
      someVar: someValue
    })
  }

  render() {
    return <Child handler = {this.handler} />
  }
}

class Child extends React.Component {
  render() {
    return <Button onClick = {this.props.handler}/ >
  }
}
```
두번째로는 외부에 있는 함수로 내부에 state를 바꾸는 경우인데 이 경우는 외부 함수 안에 콜백함수를 넣어서 
내부에서 실행할때에 콜백함수로 내부 state를 변경해주는 방법이다. 그 예시는 밑에 코드이다.
```javascript
getVideos(inputValue){
    searchYouTube({
        query: inputValue,
        max: '7',
        key: 'AIzaSyCnzXq3Qo0hR2JWG_aUiEKmkfEH8IfePyo'
      }, (target) => this.setState({
        allVids: target,
        currentVideo: target[0]
      }))
  }
```
searchYouTube함수는 외부에 있지만 callback function으로 this.state의 값을 바꿔주는 것을 볼 수가 있다.
이러한 방법들을 알아내는게 이번 sprint의 keypoint였다고 생각한다.



이번 sprint를 통해 또 얻을 수 있었던건 es6문법의 destructuring assignment에 대한 부분이었다.

예를 들면 (props)=>{props.video} 와 같은 경우에도 ({video}) => {video}와 같이 코드의 간결함을 느낄 수가 있다. 또 ()=> {this.state.videos    this.state.currentvideo} 같은 경우에도 

const {videos, currentvideo} = this.state 와 같이 처음에 선언을 해주면 

{video blah blah currentvideo}와 같이 훨씬 간결하게 사용할 수 있다. 유용한 방법이므로 예시를 아래에 코드로 적어보자면 다음과 같다.

```java	
var a = 1;
var b = 3;

[a, b] = [b, a];
console.log(a); // 3
console.log(b); // 1
-------------------------------
var o = {p: 42, q: true};
var {p, q} = o;

console.log(p); // 42
console.log(q); // true
-------------------------------
({ a, b } = { a: 10, b: 20  
console.log(a); // 10
console.log(b); // 20

```

또 react뿐만 아니라 javascript에서 유용하게 쓸 수 있는 방법 하나를 알게되었는데 혹시나 func 라는 function에 parameter를 넘기고 싶은데 바로 사용이 되어서 넘길 수가 없는 상황이 된다면 다음과 같이 function으로 한번더 감싸줘서 parameter를 넘겨줄 수 있다. 다음은 예시 코드이다.

```java	
const func = (param) => {console.log(param)}
() => {func(target)}
```



