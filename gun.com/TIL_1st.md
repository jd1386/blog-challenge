https://medium.com/@dooboolab/running-react-native-app-in-ubuntu-18-04-7d1db4ac7518

https://www.raywenderlich.com/247-react-native-tutorial-building-android-apps-with-javascript

react-native android emulator 셋팅하면서 참고한 자료들

```java	
// #1
static navigationOptions = {
    title: 'Homeaaaaaa'
    // headerTitle: <LogoTitle />
  };

// #2
static navigationOptions = ({ navigation, navigationOptions }) => {
    const { params } = navigation.state;

    return {
      title: params ? params.otherParam : 'A Nested Details Screen',
      headerStyle: {
        backgroundColor: navigationOptions.headerTintColor
      },
      headerTintColor: navigationOptions.headerStyle.backgroundColor
    };
  };
```

위의 navigationOptions 를 사용하면 title에는 상단 바에 고정될 title이 박힌다.

두번째 예시처럼 함수를 적용하여 원하는 값을 return 하는 것도 가능하다.

- 아직은 모르는 부분이 navigation에서 state와 props를 어떻게 다루는지 분석이 필요할 것 같다.



```java	
const RootStack = createStackNavigator(
  {
    Home: HomeScreen,
    Details: DetailsScreen
  },
  {
    initialRouteName: 'Home',
    defaultNavigationOptions: {
      headerStyle: {
        backgroundColor: '#82DDCB'
      },
      headerTintColor: '#fff',
      headerTitleStyle: {
        fontWeight: 'bold'
      }
    }
  }
    
    
const TabNavigator = createBottomTabNavigator({
  Home: HomeScreen,
  OrderList: OrderListScreen,
  Info: InfoScreen
});
```

createStackNavigator 와 createBottomTabNavigator는 마지막에 생성할 때 object의 key는 실제로 디스플레이에 나올 text로 적용이 되고, **value값은 component의 이름만 들어간다.**



```java	
// #1
const AppContainer = createAppContainer(RootStack);

export default class App extends Component {
  render() {
    return <AppContainer />;
  }
}

// #2
export default createAppContainer(TabNavigator);
```

디스플레이에 적용할 때는 첫번째처럼 AppContainer에 담아서 App을 export하는 경우도 있고, 두번째처럼

createAppContainer 자체를 export할 수도 있다.