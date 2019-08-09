---
layout: post
title:  '[React-Native]Navigation에 대하여'
subtitle:   'Navigation에 대하여'
categories: 'study'
tags: 'react_native'
---

웹의 경우 ``<a>`` 태그를 통해 페이지를 이동할 수 있습니다. 이는 링크 버튼을 클릭했을 때 URL이 브라저의 history stack에 쌓이고, 이전 버튼을 눌렀을 때 stack의 최상단에 있는 item을 pop해주면서 이전 페이지로 이동이 가능합니다.

React-Native는 global한 history stack과 같은 내장된 기능이 없습니다. 하지만 React Navigation을 통해 이를 구현할 수 있습니다.

가장 흔히 쓰이는 ``createStackNavigator``를 사용해보겠습니다.

---

## createStackNavigator

``createStackNavigator``는 React component를 반환하는 함수입니다.

우선 필요한 모듈을 설치해보겠습니다.

```javascript
npm install --save react-navigation
npm install --save react-native-guesture-handler react-native-reanimated
```

이후 App.js에 코드를 작성해줍니다.

```javascript
// App.js

import React from "react";
import { View, Text } from "react-native";
import { createStackNavigator, createAppContainer } from "react-navigation";

class HomeScreen extends React.Component {
  render() {
    return (
      <View style={{ flex: 1, alignItems: "center", justifyContent: "center" }}>
        <Text>Home Screen</Text>
      </View>
    );
  }
}

const AppNavigator = createStackNavigator({
  Home: {
    screen: HomeScreen
  }
});

export default createAppContainer(AppNavigator);
```

실행을 해보면 다음과 같이 출력됩니다.

![](/assets/img/posts/2019-08-02-16-43-42.png)

