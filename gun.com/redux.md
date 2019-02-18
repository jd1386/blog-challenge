이번 스프린트에서 마지막에 고민했던 부분은 filter를 이용하여 todolist중에 완료된 것들과 안된것들을 따로 화면에 비춰주는 함수였다. 다음 코드를 보면서 이해해보면, 

```java	
<span id="SHOW_COMPLETED" className="filter" onClick={(e) => {
        onVisibilityFilter(e.target.id)
        filterFunc(e.target.id)
      }}>COMPLETED</span>
```

filterFunc는 argument가 show_all, show_completed, show_active 중 어떤 것인지 확인한 후 그에따라 화면에 비추는 모습을 filter해주는 함수인데, 처음에는 이 argument를 state의 filter로 넣었었는데, 작동하지 않았다. 

그 이유가 중요한데 console.log를 통해 확인해보니 onVisibilityFilter 함수가 실행되고나서 state.filter를 찍어보니 아직 변경되지 않은 상태였고, 변하지 않은 값으로 filterFunc가 실행되고 있었다. 그렇기 때문에 내가 원한 의도로 코드가 실행되지 않은 것이었다. 그래서 위와 같이 변경하니 코드가 내 의도대로 실행되었다.



App(보통 가장 상위 컴포넌트)를 index.js에서 Provider로 감싸고 provider에 store={store} 로 담아주면 App 하위에 있는 컴포넌트들이 어디서든 store에 접근할 수 있다.



mapToDispatch를 한 곳에 몰아서 써야할지 아니면 필요한 곳들에 분산시켜서 써야할지 고민했었는데 필요한 곳마다 쓰는게 유지보수하기에 훨씬 편하다고 하니 분산시켜서 써놓아야 할 것 같다.



```java	
const store = createStore(reducers, window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__());
```

#### **위와 같이 store를 넘겨주면 크롬개발자도구에서 redux의 활동을 하나하나 다 볼 수 있다.



### redux의 각 repo의 역할

action은 무슨일이 일어났다만 정보만 담음

reducer에서 일을 함

예상해놓은 액션만 행동을 함

dispatcher가 교통정리를 함

redducer는 순수함수다(같은 input에는 같은 output을 줌)

항상 dispatch 함수를 거쳐 reducer에 가야한다.(유일한 길이다)
 

reducer에선 dispatch하면 안된다.  

**redux의 장점: 한방향으로 가는건 디버깅이 용이함.**

Object.assign은 (a,b,c) a,b,c라는 object를 다 통합시켜줌 같은 값이 있으면 마지막 c의 값이 최종값
  

reducer에 있는 함수가 한개면 초기값이 object하나니까 가리킬때 state.value와 같이 한번에 가리키면 되지만

함수가 두개면 combine시켜줬으니까 가리킬 때 state.counter.value와 같이 한번더 거쳐서 가리켜야한다.


  