#### react-native expo deployment

app.json에 가면 expo 배포에 대한 설정이 있는데, 이중에 expo.name은 앱이 배포되고 다운받았을 때의 앱 이름이 된다.

expo.icon은 다운로드 되었을 때의 아이콘, splash.image는 로딩 이미지를 의미한다.

이때 중요한 점이 name과 slug를 바꿔주면 expo가 다른 프로덕트로 인식하게 되는데 이렇게 되면 프라이빗 키가 달라져서 같은 프로젝트로 업데이트하고 싶을 때 그렇게 하지 못한다. 따라서 구글 플레이 스토어에서 같은 프로젝트로 업데이트 하고 싶다면 name과 slug를 유지하며 프로젝트를 진행해야 한다.

#### ** 가장 많이 헤맸던 부분: AsyncStorage의 값을 어떻게 navigationOptions에서 사용할 것인가

이 부분에 대해선 고민이 많았는데 처음 시도했던 방법이 AsyncStorage의 값을 state에 담은 후 navigationOptions에 담는 것이었다. 그런데 이 부분에서 일어나는 문제가 navigationOptions의 설정을 render가 되기 전에 state 설정이랑 같이 해줬기 때문에 state를 아직 define 하지 않았다고 인식해서 this.state를 쓸 수가 없었다. 

그래서 시도한 방법이 componentDidMount를 이용하여 props.navigation.params 라는 곳에 저장하고 그 값을 불러오는 방식이었다. 이 해결책을 코드로 옮기면 다음과 같다.

```javascript
static navigationOptions = ({ navigation }) => {
    // 37th line prevent that 'address' is null
    return {
      headerTitle: (
          <Text style={{ fontSize: 18, fontWeight: "bold" }}>
            {navigation.getParam("address")
              ? navigation.getParam("address")
              : "주소를 입력하세요."}
          </Text>
      )
    };
  };

  //this is changing value of this.props.navigation.params
  componentDidMount() {
    AsyncStorage.getItem("address", (err, result) => {
      this.props.navigation.setParams({
        address: result ? result : "주소를 입력하세요."
      });
    });
  }
```

위와 같이 setParams로 params에 data를 저장하고 이를 headerTitle에서 출력하는 방식을 사용하면 AsyncStorage의 값을 navigationOptions에서 불러올 수 있다.