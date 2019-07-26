---
layout: post
title:  '[ReactNative]Component에 대해서'
subtitle:   'Component에 대해서'
categories: 'study'
tags: 'react_native'
---

본격적으로 앱을 만들어 보겠습니다. 
그렇다면 가장 기본적인 구성요소인 **Component**에 대해 알아보도록 하겠습니다.

Component는 화면을 구성하는 하나의 단위입니다. 하나의 컴포넌트는 독립적으로 존재할 수도 있고, 컴포넌트들이 모여서 새로운 컴포넌트를 만들 수도 있습니다.

---

# Component

Component는 JSX라는 문법을 기반으로 작성됩니다. JSX란 Component를 좀 더 쉽게 작성할 수 있도록 React에서 제공해주는 문법입니다. HTML의 태그와 비슷한 모양을 가지고 있습니다. 다만 React할 때 HTML 태그를 사용할 땐 아무런 절차 없이 사용할 수 있었지만, React-Native는 사용하고 싶은 컴포넌트를 명시적으로 import 해줘야 합니다.

```javascript
// Text를 사용하기 위해선 명시적으로 import
import { Text } from 'react-native';

<Text onPress={this.onPressTitle}> 클릭클릭 </Text>
```

컴포넌트는 <태그></태그> , 내용이 없을 경우 <태그 />의 모양으로 이루어져 있습니다.

위의 코드중 ``onPress``는 Text 컴포넌트의 속성에 해당됩니다. 사용자가 해당 컴포넌트를 눌렀을 경우 ``{this.onPressTitle}``을 반환합니다. ``{this.onPressTitle}``은 함수 이며, javascript 값을 사용하기 위해선 ``{}``로 감싸줘야합니다.

## 프로젝트 생성

```
create-react-native-app n_test
```

그리고 ``App.js`` 파일을 열어봅시다.
``App.js``는 yarn start를 했을 때 가장 먼저 찾는 파일입니다. 즉 가장 메인이 되는 파일입니다.

![](/assets/img/posts/2019-07-26-14-37-54.png)

```javascript
//App.js

import React from 'react';
import { StyleSheet, Text, View } from 'react-native';

//App이라는 class를 만들고 이를 export합니다.
export default class App extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        <Text>React-Native</Text>
      </View>
    );
  }
}

//style을 설정해줍니다.
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
});
```

실행을 하면 다음과 같이 나옵니다.

![](/assets/img/posts/2019-07-26-14-47-35.png)

## 코드 이해하기

위의 코드는 다음과 같이 해석할 수 있습니다.

```javascript
상자에 담아서{
	보여준다(){
		우리가 만든 부품: (
      <View style={styles.container}>
        <Text>React-Native</Text>
      </View>
		);
	}
}

//위의 내용을 React-Native가 알아듣게 바꾸면 이렇게 됩니다.
export default class App extends React.Component{
  render() {
    return (
      <View style={styles.container}>
        <Text>React-Native</Text>
      </View>
    );
  }
}
```

## View & Text Component

```javascript
// 1. HTML로 화면 그리기
<div style="border:1px">
	<p>React-Native</p>
</div>

// 2. React Native로 화면 그리기
<View style={{borderWidth:1}}>
  <Text>React-Native</Text>
</View>
```

### View 

도화지 컴포넌트 입니다. View는 HTML의 div의 역할을 합니다.

### Text

문자를 표현할 때 사용하는 컴포넌트입니다.

