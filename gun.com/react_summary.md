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

또한 async와 await에 대한 정리인데 아직 완벽히 숙지가 되지 않은 개념이지만 현재까지의 이해로 작성해본다면 async는 비동기적으로 함수를 실행하기 위해 앞에 달아주는 것뿐이고 await는 그 부분에서 멈춰있다가 해당부분에 제대로 된 값이 들어오면 그 후에 다음 코드들을 실행해 주는것 같다.

```java	
_getMovies = async () => {
    const movies = await this._callApi();
    this.setState({
      movies
    });
  };

  _callApi = () => {
    return fetch(
      "https://yts.am/api/v2/list_movies.json?sort_by=download_count"
    )
      .then(potato => potato.json())
      .then(json => json.data.movies)
      .catch(err => console.log(err));
  };
```



React에서의 fetch에 대한 부분도 짚고 넘어갈 필요가 있는데, 내가 사용했을 때는 fetch를 통해 Data를 state의 한 속성으로 넘겨주는 것이 가장 효율적이었다. 하지만 상속을 해주는 자식 컴포넌트 또는 파일에서 fetch로 받아온 후 state를 변경시켜줘야 할 경우도 있는데 그땐 callback으로 바꾸어 주면 된다.

```java	
//fetch로 state변경하는 예
_callApi = () =>{
	fetch(url)
        .then(res => res.json())
        .then(json => this.setState({
            movies
        }))
}

//자식에서 fetch로 변경하는 예
//자식
_callApi = (callback) => {
	fetch(url)
        .then(res => res.json())
        .then(json => callback(json))
}
//부모
getData = () => {
    _callApi((target) => this.setState({
        movies: target
    }))
}
```

