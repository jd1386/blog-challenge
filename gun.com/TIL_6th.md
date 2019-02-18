#### react native의 Alert 

react native의 Alert은 여러가지 기능이 있는데 그 기능과 기본적인 형태가 다음과 같고, 그 아래는 예시의 display screen이다.

```javascript
 Alert.alert('입력이 완료되었습니다.', '내용?', [
                {
                  text: '나는 텍스트',
                  onPress: () =>
                    this.props.navigation.navigate('HomeScreen', {
                      address: storageAddress
                    })
                }
              ]);
```

이때 마지막 parameter가 array안에 object이고 text값의 default는 운영체제마다 갖고 있다는 것을 알고 있어야 한다.

(ios는 OK)

![Image from iOS](/home/yugeon/Downloads/Image from iOS.png)



#### react-native-google-places-autocomplete

npm에 위와 같은 모듈이 존재한다. 이는 google api를 이용하여 input을 만들어서 input에서 주소를 자동완성해준다. 

다음의 코드와 주석은 자동완성 input을 만드는 과정이다.

```java	
<GooglePlacesAutocomplete
      placeholder="Search"
      minLength={2} // minimum length of text to search
      autoFocus={false}
      returnKeyType={'search'} // Can be left out for default return key https://facebook.github.io/react-native/docs/textinput.html#returnkeytype
      listViewDisplayed="auto" // true/false/undefined
      fetchDetails={true}
      renderDescription={row => row.description} // custom description render
      listViewDisplayed={false} // 리스트중 하나를 누르면 리스트가 없어짐
      onPress={data => {
        onPress(data.description);
      }}
      getDefaultValue={() => ''}
      query={{
        // available options: https://developers.google.com/places/web-service/autocomplete
        key: 'AIzaSyARsT1ginurAWCY0B6NES8NG7X_HpSuYDI',
        language: 'ko', // language of the results
        types: '(regions)' // default: 'geocode'
      }}
      styles={{
        textInputContainer: {
          width: '90%',
          marginLeft: 20
        },
        description: {
          fontWeight: 'bold'
        },
        predefinedPlacesDescription: {
          color: '#1faadb'
        }
      }}
      // currentLocation={true} // Will add a 'Current location' button at the top of the predefined places list
      // currentLocationLabel="Current location"
      nearbyPlacesAPI="GooglePlacesSearch" // Which API to use: GoogleReverseGeocoding or GooglePlacesSearch
      GoogleReverseGeocodingQuery={
        {
          // available options for GoogleReverseGeocoding API : https://developers.google.com/maps/documentation/geocoding/intro
        }
      }
      GooglePlacesSearchQuery={{
        // available options for GooglePlacesSearch API : https://developers.google.com/places/web-service/search
        rankby: 'distance',
        types: 'food'
      }}
      filterReverseGeocodingByTypes={[
        'locality',
        'sublocality',
        'postal_code',
        'country',
        'administrative_area_level_1',
        'administrative_area_level_2'
      ]} // filter the reverse geocoding results by types - ['locality', 'administrative_area_level_3'] if you want to display only cities
      predefinedPlaces={[]}
      debounce={200} // debounce the requests in ms. Set to 0 to remove debounce. By default 0ms.
    />
```

진행하던 프로젝트에선 한글만을 지원하는 프로젝트였으므로 language를 korean으로 설정하였고, 검색하는 types을 region으로 설정했다. 이의 default 값은 geocode이고 region의 특성은 넓은 범위에서의 검색을 해준다는 점에 있다.

또 listViewDisplayed={false} 이 부분이 중요한 역할을 하는데, 내가 검색된 내용중 하나를 선택하면 원래 리스트를 안보이게 해주는 역할을 한다. 



#### react-native fade-in, out animation

```javascript
state = {
    number: 1,
    fadeIn: new Animated.Value(0),
    fadeOut: new Animated.Value(1),
    Y: 100
  };
  fadeOut() {
    this.state.fadeIn.setValue(1);
    Animated.timing(this.state.fadeIn, {
      toValue: 0,
      duration: 500
    }).start();
  }(

render(){
    return(
  		 <Animated.View
          style={{
            opacity: this.state.fadeIn
          }}
        >
          <View style={{ marginTop: 30, width: 50 }}>
            <Text style={{ fontSize: 15, textAlign: 'center' }}>+1</Text>
          </View>
        </Animated.View>
		<TouchableOpacity
            onPress={() => {
              this.fadeOut();
              this.setState({ number: this.state.number + 1 });
            }}
            style={{ marginLeft: 40 }}
          >
            <Text style={{ fontSize: 30 }}>+</Text>
          </TouchableOpacity>
  )
}
```

위와 같이 fadein과 fadeout animation을 구현할 수가 있다.