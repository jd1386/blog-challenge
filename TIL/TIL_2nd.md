git pull origin master --allow-unrelated-histories 라는 keyword를 사용하면 연결이 없는 것 같아도 당겨올 수 있다.

git init 후 git push origin master가 안되는 상황에서 위의 명령어를 사용했더니 다 origin에  올릴 수 있었다.



createStackNavigator를 쓸때는 페이지를 하나를 만들어 주는 것과 같은 역할이므로 한번만 쓰고 하위에 있는 컴포넌트 들은 상위의 페이지를 받아서 써야한다. 그래서 HomeScreen이라는 component에 다음과 같은 페이지가 있으면

```java	
export default createStackNavigator({
  HomeScreen,
  Address,
  RestaurantLists,
  Restaurant
});
```

RestaurantLists 라는 컴포넌트에서 

```java	
onPress={() => this.props.navigation.navigate('Restaurant')}
```

위와 같이 props로 위에 있는 것을 받아서 사용할 수 있다.



문서들을 보다보면 navigation.navigate를 쓸 때 해당 컴포넌트를 stateful한 컴포넌트로 쓸 때가 많은데 사실 stateless한 컴포넌트로 사용해도 상관없다.



```java	
const TabNavigator = createBottomTabNavigator({
  홈: {
    screen: HomeScreen,
    navigationOptions: {
      tabBarIcon: ({ focused, tintColor }) => (
        <Image
          source={require('./SAMPLE.png')}
          style={{ width: 25, height: 25 }}
        />
      )
    }
  }
```

createBottomTabNavigator를 할 때 navigationOptions의 tabBarIcon의 값을 주면 image를 tab에 넣을 수 있다.



**git push upstream master:feature 로 하면 내 마스터를 upstream의 feature로 푸쉬한다.**