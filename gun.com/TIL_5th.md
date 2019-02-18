** **react router 에서의 중요한 특징: Route 뒤에 exact를 붙여주지 않으면 path='/'인 기본 라우터가 어떤 라우터에서든 렌더링이 된다. 따라서 기본 Router를 띄워줄게 아니면 exact를 꼭 써줘야한다.**

```javascript
//예시
<Route exact path="/" component={App} />
<Route exact path="/signup" component={Signup} />
```



#### react-native-tab-view

react-native-tab-view라는 모듈이 있는데 배달의 민족에서 카테고리를 옆으로 swipe하면 넘어가는 화면을 구현하는 모듈이다. 사용방법의 예시는 다음과 같다.

```javascript
import * as React from 'react';
import { View, StyleSheet, Dimensions } from 'react-native';
import { TabView, TabBar, SceneMap } from 'react-native-tab-view';
 
const FirstRoute = () => (
  <View style={[styles.scene, { backgroundColor: '#ff4081' }]} />
);
const SecondRoute = () => (
  <View style={[styles.scene, { backgroundColor: '#673ab7' }]} />
);
 
export default class TabViewExample extends React.Component {
  state = {
    index: 0,
    routes: [
      { key: 'first', title: 'First' },
      { key: 'second', title: 'Second' },
    ],
  };
 
  render() {
    return (
      <TabView
        navigationState={this.state}
        renderScene={SceneMap({
          first: FirstRoute,
          second: SecondRoute,
        })}
        animationEnabled={false} // 화면 넘기는 animation를 disable
 		swipeEnabled={false} // swipe를 disable 
        onIndexChange={index => this.setState({ index })}
        initialLayout={{ width: 0 }}
      />
    );
  }
}
 
const styles = StyleSheet.create({
  scene: {
    flex: 1,
  },
});
```



#### onBlur 기능

input에 onBlur라는 기능이 있는데 커서가 해당 input에서 벗어났을 때 그안의 함수를 실행시킨다. 비밀번호가 비밀번호 확인과 일치하는지 text를 띄워주는 부분을 onBlur를 이용했다.



#### AsyncStorage.getItem

```javascript	
_getData = async () => await AsyncStorage.getItem('data')
let result = _getData()
```

위와 같이 asyncstorage에 콜백을 쓰지않고도 원하는 data를 비동기 처리하여 받아올 수 있다.

