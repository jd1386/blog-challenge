#### 모바일의 localStorage인 AsyncStorage
mobile 에서의 localstorage는 AsyncStorage라는 것이 있다. web의 localstorage와 마찬가지로 같은 기기면 클라이언트를 껐다가 켜도 그대로 정보가 유지된다. 사용하는 방법은 다음과 같다. 

```java	
//정보를 저장할 때
AsyncStorage.setItem('key', 'value')
//정보를 가져올 때
AsyncStorage.getItem('key', (err,result) => {
    console.log(result) // result가 원하는 값
})
//정보를 지울 때 
AsyncStorage.removeItem('key')

// 위의 함수들은 다 비동기이기 때문에 원하는 처리 순서가 있다면 비동기 처리를 해줘야 한다.
//ex 
async getItemValue(key){
    try{
        await AsyncStorage.getItem('key', (err,result) => {
            console.log(result);
        })
    }
    catch(err){
        throw err;
    }
}
```

***주의할 점은 web에서의 localStorage와 같이 string으로 저장이 된다는 점이다 그래서 array나 object를 저장하고 싶을땐 JSON.stringify를 한 후 저장하고 찾아올 때 가져와서 parse해줘야 한다.**

이번 프로젝트에서는 장바구니와 주소변경을 할 때 위의 storage를 썼다.



#### navigator를 이용할 때 data를 넘겨주는 방법

navigator를 이용해서 page를 이동할 때 어떤 data를 하위 페이지 또는 상위 페이지로 넘겨주는 방법을 모색하다가 찾은 방법이 있다. 그 방법은 아래와 같다.

```java	
// 다른 페이지로 넘어갈 때 data를 싣는 상황 (currentPage.js)
onPress={() => {
    this.props.navigation.navigate('anotherPage', {
        data: this.state.data
    })
}}

// anotherPage.js
const { navigation } = this.props;
const data = navigation.getParam('data');
//이런 방법으로 data를 받은 후 anotherPage에서 data를 사용할 수 있다.
```



#### StyleSheet 작성방법

```java	
import { View, Text, StyleSheet } from 'react-native';

const Some = () => (
	<View>
		<Text style={styles.item}></Text>
    </View>
)


const styles = StyleSheet.create({
    item: {
        fontSize: 25,
        marginTop: 15,
    	marginLeft: 15
    }
})
   
```

위와 같은 방식으로 styleSheet를 작성한다면 같은 style을 여러번 쓰지 않고 한번에 작성할 수 있다.

(코드의 재사용성, 유지.보수가 쉬워진다.)



#### react native에서의 Alert.alert과 alert의 차이

Alert.alert('')은 괄호안의 값만 알림으로 뜨지만, alert('')은 알림에 Alert이라는 문자가 같이 나온다.



#### StackNavigator를 사용하는 방법

처음에 이 navigator를 사용할 때 상위 페이지에 createStackNavigator를 올려주고 상위는 또 createStackNavigator를 올려주는 방식으로 생각했었는데 그렇게 하면 페이지가 여러개가 생기면서 페이지 안에 또 다른 페이지가 생기고 보기 싫은 페이지가 나온다.

그래서 생각한 방법이 createStackNavigator는 가장 상위에 두고 그 안에 내가 옮겨다니고 싶은 페이지를 다 넣은 후 각 component들에서는 component 자체만을 export 시켜주는 것이다. 그 예시를 보면 다음과 같다.

```java	
// HomeScreen.js
import React, { Component } from 'react';
import Address from './Address';
import Restaurant from './Restaurant';     
class HomeScreen extends Component {
}
export default createStackNavigator({
    HomeScreen,
    Address,
    Restaurant
})
    
// Address.js
import React from 'react';

const Address = (props) => (
 <Button 
 onPress={() => {
 props.navigation.navigate('Restaurant');
 }}
 />
)

export default Address;

// Restaurant.js
import React from 'react';
const Restaurant = () => (
<Some>
)
export default Restaurant;

```



#### react native에서 button안의 text나 button자체의 크기를 조절하기

react native에서의 button은 크기가 정해져 있어서 마음대로 text의 크기를 조절한다거나 자체의 크기를 조절하는 것이 어려웠다. 그래서 찾아낸 방법은 touchableOpacity를 사용하는 방법이었는데 다음과 같이 하면 크기를 조절하기 편하다.

```jav	
// 원래 시도했던 방법
<Button title="sample" style={{fontSize: 50}} /> //style이 원하는 방향으로 적용되지 않음

// 해결방법
<TouchableOpacity style={{width:60, height:60}}>
	<Text style={{fontSize:50}}>sample</Text>
</TouchableOpacity>
```



#### ScrollView안에서 정적인 아이콘 만들기

이번 프로젝트에서 장바구니의 위치가 스크롤 뷰 에 같이 있는 것 같으면서 스크롤이 내려갈 때 같이 딸려가지 않게 위치를 지정해줘야 했다. 그래서 사용한 방법이 위치를 absolute로 주는 것이었는데 실제로 사용한 코드는 다음과 같다.

```javascript
<ScrollView>
	<Some />   
</ScrollView>
<TouchableOpacity style>
	<Image source={{uri:'https://www.someurl.com'}}
</TouchableOpacity>
```



