# React Native :: 0. Introduction
#3_out/dev/React-Native
#5_data/date/2019/12/05

## 0. Introduction
현재 날씨를 알려주는 React-Native기반 앱을 만들겁니다.

## 1. Requirements
- node.js @ 12.0.0 ^
- npm @ 6.9.0 ^
- expo-cli
`npm install -g expo-cli`

- simulator를 위한  `xcode `, `android` 혹은 ios, android 기기

## 2. Expo vs RN CLI
expo는 React-Native를 위한 설정 파일같은 것들이 없는 방식으로, 모든것이 셋업 되어있다. 만약에 React-Native(RN) CLI를 수동으로 작업하고 싶다면,  node, watchman, react-native-cli를 인스토 하면 된다. [Getting Started · React Native](https://facebook.github.io/react-native/docs/getting-started) 공식 문서를 보고 따라하면 된다.

RN CLI 방식은 Native file을 더 많이 컨트롤 하고 싶을때, 사용하면 된다. Xcode, Android 파일을 생성할꺼고, 양쪽 파일들이 RN에서 실행될것이다.  이때 RN CLI로 작업을 할 경우 양쪽 파일들에 다 접근을 할 수 가 있기 때문에, 어떤 떄는 둘을 결합할 수도 있다.

반면에, Expo는 모든 Native files들을 숨기고, 해당 요소들을 Expo에서 관리한다. 이것이 Expo의 가장 큰 장점이자. 단점이다. 

Expo를 사용하면 빠르게 작업(디버깅, 시뮬레이션 확인을 포함.)  할 수 있지만, RN CLI로 작업할 경우 개발자 계정, Xcode Connect등 몇가지 요구조건이 있다. 숙련된 개발자가 아니라면, expo를 추천한다. 숙련된 개발자도 RN CLI 방식으로 작업할 경우 많은 버그를 만나게 됨으로. 되도록 Expo를 활용해서 만드는것을 추천한다.

Expo에서 작동하는 Api들이 RN에서는 직접 구현해야 할 수 있다. 

> 개인적 견해로는 Expo로 시작해서 RN방식으로 넘어가는것도 괜찮다고 생각한다. Expo에서 미리 만들어논 라이브러리를 바탕으로 앱 개발을 해보고 RN방식으로 넘어가 구현되어 있지 않은 부분을 Expo를 참고하여 만드는 것도 좋은 방법이라고 생각이 든다.

## 3. Creating the Project
expo project를 만들기 위해서는 expo cli 에서 init 명령어를 통해서 생성한다. `expo init` expo에서 typescript를 사용 가능한데, 허나 우리는 이것을 모름으로 blank형태로 만든다. 옵션은 4가지가 있는데 설명을 읽어보도록.

생성하고나면 app.json 파일이 형성될 것이다.
```json
{
  “expo”: {
   	…
    “platforms”: [
      “ios”,
      "android",
      "web”
    ],
		…
    }
  }
}
```
expo에서 제공하는 플랫폼은 3가지가 있다. iOS, android, web(beta). `yarn start` `npm run start`명령어를 사용하여 어플리케이션을 실행해보자.
실행하면, expo DEV Tools 를 자동으로 로딩해준다.
[image:6064C791-2706-402C-9DB7-D925189FD47D-340-0000125DBED6929A/EC2AAE51-9257-4FA9-ABAD-D1635BDD6C31.png]
QR코드를 이용해서 기기에서 직접 실행해보거나, Android Studio 혹은 Xcode를 이용해서 어플리케이션 결과를 바로바로 확인 할 수 있다.

## 4. Getting to know Expo
expo는 live reloading과 hot reloading을 지원한다. 소스코드에 변경이력이 생기면, expo가 그것을 감지하고 바로 바로 피드백을 주는 형태이다.
[javascript - What is the difference between Hot Reloading and Live Reloading in React Native? - Stack Overflow](https://stackoverflow.com/questions/41428954/what-is-the-difference-between-hot-reloading-and-live-reloading-in-react-native)

live reloading은 앱을 구현하는 파일이 변경되었을 때 시스템을 재시작하여 이를 반영하는 형태이다. hot reloading은 app내에 state 정보를 남겨둔체 style만 반영해주는 형태라고 생각하면된다. 앞으로 개발을하며, 이를 차차 알아가자.

## 5. How does React Native
모바일 앱을 만드는 3가지 다른 방법이 존재한다.

1. Native
	- Swift or Object-c를 이용하여 IOS 앱을 만드는 것.
	- java or Kotlin을 가지고 Android 앱을 만드는 것.
2. Cordova or PhoneGap 하이브리드 앱
	* 앱 컨테이너 내부의 HTML, CSS를 직접적으로 넣는 방식. 반응형 웹 이 잘 구현되어진 홈페이지의 어플리케이션을 만들거나 Native앱을 만들 자원(인력, 자금)이 부족한 경우 이렇게 만듬.
	* Native기능을 사용하는데 매우 제한적이다.
3. React-Native
	- Android, IOS는 기본적으로 자바스크립트 엔진을 가지고 있어서 자바스크립트를 실행 할 수 있다. 이를 이용하여 Native 엔진에 메세지를 보내는 방식. 일종의 브릿지 역할을 한다.
	- 웹을 React로 개발할때의 컴포넌트와 CSS 엔진등을 적용 할 수 있게 해준다.
	- 단, Native로 직접 접근하는 것이 아닌 간접적으로 접근 하기 때문에 항상 브릿지를 거쳐야 Native의 기능을 사용할 수 있다. 그러므로 효율적으로 Native 기능을 사용할 때 브릿지를 통한 방식은 부하가 걸려 성능 저하를 이야기 할 수 있음으로 적합하지 않다.
	- 또한, React의 문법을 허용하되 완전하게 똑같이 구성되지 않는다 예를 들어 CSS적용이라던지 Component의 구성방식이 정해져 있다. React-Native 브릿지는 자바스크립트 객체를 Native로서 실행가능하도록 변화시키는 특정한 규칙을 가져있기 때문이다.
# React Native :: 1. Logic
#3_out/dev/React-Native
#5_data/date/2019/12/05

## 0. Layouts with Flexbox in React Native
#### Style.
React Native에서는 CSS엔진을 구현해두었다. 완전 동일하게 CSS 작동하지는 않지만, 유사하게 작동함.
사용하는 방법,
```javascript
import {StyleSheet} from ‘react-native';
…
<View style={styles.container}>
	<Text style={styles.text}>Sikso</Text>
</View>
…
const styles = StyleSheet.create({
	container:{
		flex: 1
	},
	text:{
		fontWeight: ‘bold’
	}
})
```
주의사항으로는 Style도 자바스크립트 객체 형태로 적용이되며, caMel case로 선언하거나, 자식요소로 전달되지않는다거나 등등은 실제로 개발하는 단계에서 문서를 찾아보고 검색하면서 흐름을 잡아가면 될거 같다. 이에 관하여 나중에 정리하면 되겠다. 

#### Flexbox.
그러면, 본격적으로 React Native에서는 어떠한 방법으로 레이아웃을 설정하는지 알아보자. 앞서 언급한 Style에서  FlexBox요소가 있다. 여러가지 옵션이 있지만, 기본적인 `flex`에 대해서 살펴보자. `flex`는 간단하게 요약하면 비율을 의미한다. 해당 설정된 요소를 부모요소로부터 어떠한 비율로 배치할 지를 의미한다.

예를 들어 3개의 컴포넌트를 배치할때 각각 `flex`1,1,2 라고 한다면 각 컴포넌트는 1 : 1 : 2의 비율로 배치가 된다. 이는 실습에서 쉽게 알아볼수 있을 것이다.

이 Flex와 관련된 properties가 다양한데 몇가지를 소개한다면, FlexDirection 자식들을 어떻게 배치할지, default로는 column이다.`flexDirection: ‘row’`를 사용하면 자식요소들의 배치가 가로로 배치한다. 그외에도 `justifyContent`,`alignItems`,`flexWrap`,`noWrap`등이 있다.

레이아웃을 잡는 다른 방법도 있지만, flex를 적극적으로 활용하기를 바란다. 비율로 접근하는건 매우 Fuxx하니깐,

React-Native가 제공하는 Api문서는 다음 링크에서 볼 수 있다.[Layout Props · React Native](https://facebook.github.io/react-native/docs/layout-props.html)

## 1. Loading Screen
해당 섹션을 진행하기 앞서 React에대한 다음과 같은 이해가 필요하다. [함수형 컴포넌트와 클래스, 어떤 차이가 존재할까? — Overreacted](https://overreacted.io/ko/how-are-function-components-different-from-classes/) 우선 이런게 있다고만  생각하고 컴포넌트를 구성하는 방법이 두가지가 있는데 앞으로 클래스로 컴포넌트를 구성하려고 합니다. 해당 부분에 대해서는 나중에 컴포넌트를 구성하는 방법에 대해서 React 를 공부하며, 익히는것으로 합시다. 

외부에서 만들어진 컴포넌트를 추가 할 수 있습니다. [코드 분할 – React](https://ko.reactjs.org/docs/code-splitting.html) 방법을 참고하여 다음과 같이 구성합니다.
```bash
Root
- app.js
- loading.js
```
새롭게 loading 컴포넌트를 외부에서 만들어서 메인 컴포넌트가 되는 app.js에서 불러와서 사용하는 방법으로 접근합니다.

```javascript
import Loading from ‘./loading'

export default class app extends React.Component{
	render() {
		<View><Loading/></View>
	}
}  
```

## 2. Getting the Location
 우리가 구현하려고 하는 logic에 대해서 생각해보자 사용자가 현재 있는 위치 기반을 바탕으로 우리는 날씨를 표현하고 싶다. 이것에대한 구현하기 위한 로직을 우리는 간단한 로직을 생각 할 수 있습니다.

	1. 사용자 현재 위치를 가져온다.
	2. 사용자 현재 위치를 이용하여 날씨 정보를 가져온다.

#### 사용자 현재 위치 가져오기.
React-Native Api에서 해당 정보를 가져오는 방법을 찾아봅시다. Geolocation이라는 모듈안에 여러가지 정보를 가져올 수 있습니다. 이중에 우리가 [Geolocation · React Native](https://facebook.github.io/react-native/docs/geolocation) api 문서를 보고 구현 할 수 있다.

Expo는 React-Native에서 사용되는 확장시킨 형태이다. 우리는 Vanilla React-Native에서 사용되는 Geolocation이 아닌 Expo의 확장 버전을 [Location · Expo](https://docs.expo.io/versions/v35.0.0/sdk/location/)사용한다. 해당 라이브러리를 가져오기 위해서 [다른 라이브러리와 통합하기 – React](https://ko.reactjs.org/docs/integrating-with-other-libraries.html) 다음을 참고하자. 요약하면, 우리가 사용하는 componentDimMount() 함수는 render()함수가 끝난 후 불리는 함수이다. 즉, 커스텀으로 만들어진 컴포넌트를 완성후 외부에 컴포넌트를 부르려고 사용되는것 같다. 

> 해당 내용을 자세히 알고 싶다면  [리액트 교과서 - 컴포넌트와 라이프사이클 이벤트](https://velog.io/@kyusung/%EB%A6%AC%EC%95%A1%ED%8A%B8-%EA%B5%90%EA%B3%BC%EC%84%9C-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EC%99%80-%EB%9D%BC%EC%9D%B4%ED%94%84%EC%82%AC%EC%9D%B4%ED%81%B4-%EC%9D%B4%EB%B2%A4%ED%8A%B8)과 리액트 라이프사이클을 통해서 찾아보면 될 것 같다.  

`expo install expo-location`을 사용해서 해당 라이브러리를 설치하자. `npm`,`yarn`도 가능할것 같다 그래도 `expo`를 사용하는 이유는 해당 모듈로 설치하는것을 권장하고 있기 때문인것 같다. 똑같은 역할을 한다.

> 개별적으로 설치하는 이유는 expo에는 수많은 라이브러리들이 있다 이것을 전부 앱에 넣어놓고 사용하기에는 너무 무겁기때문에 필요한 모듈만 설치하여서 사용하도록 되어 있다.  

해당 작업이 끝난 후 실행을 해보면 Permission error가 나온다. 이것을 해결하는 방법을 밑에서 계속해서 서술하겠다.

## 3. Asking for Permissions
앞서 사용한 expo-location은 사용자의 permission을 요구한다. 왜냐하면 우리가 일반적으로 앱을 사용할때 사용자 위치정보 기반의 허가 여부를 물어보는것처럼 앱에서 마구 잡이로 사용자 정보를 수집할 수 없도록 막아논것 같은 뇌피셜 뇌피셜.

그래서 사용자에게 permission을 요구하는 함수를 location api에는 서술되어 있다. 

> You must request permission to access the user's location before attempting to get it. To do this, you will want to use the  [Permissions](https://docs.expo.io/versions/v35.0.0/sdk/permissions/)  API. You can see this in practice in the following example.  

[Permissions - Expo Documentation](https://docs.expo.io/versions/v35.0.0/sdk/permissions/) 해당 내용에서 location permission을 찾는 부분을 살펴보자. 문서에서는 두가지 방법이 존재한다고 한다. 나는 Location.requestPermissionAsync()를 이용하여 구현하였다.

> `Location.requestPermissionsAsync()`Requests the user for location permissions, similarly to `Permissions.askAsync(Permissions.LOCATION).`  

## 4. Getting the Weather
위치정보를 가져왔다. 신난다. 오픈api를 활용해서 날씨정보를 가져오자. 유명한 날씨 api가 있다. [Сurrent weather and forecast - OpenWeatherMap](https://openweathermap.org/) 여기서 날씨정보를 가져올 수 있다. 해당 문서를 읽어보면 api 사용법이 나올것이다. 계정을 만들어서 api key를 읽어오고 해당 key와 우리가 앞서 읽어온 위경도를 활용하여 해당 위치에 날씨정보를 반환받을 수 있다.

Node.js에서 자주 사용되는 모듈로 axios라는 모듈이 있다.[GitHub - axios/axios: Promise based HTTP client for the browser and node.js](https://github.com/axios/axios)자세한 내용은 여기 있으며, 실습 코드를 통해서 어떠한 방법으로 전송하는지 살펴보자.
