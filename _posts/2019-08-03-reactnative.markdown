---
layout: post
title:  '[React-Native]Tab-Navigation'
subtitle:   'Tab-Navigation'
categories: 'study'
tags: 'react_native'
---

navigation에서 하단 Tab navigation을 구현하는 방법을 알아보겠습니다.

---

App.js에 다음과 같이 코드를 입력해줍니다.

```javascript
import React from 'react'
import { Text, View } from 'react-native'
import { createBottomTabNavigator, createAppContainer } from 'react-navigation'

class HomeScreen extends React.Component {
    render(){
        return (
            <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
                <Text>Home!</Text>
            </View>
        )
    }
}

class SettingsScreen extends React.Component {
  render() {
    return (
      <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
        <Text>Settings!</Text>
      </View>
    )
  }
}

const TabNavigator = createBottomTabNavigator({
  Home: { screen: HomeScreen },
  Settings: { screen: SettingsScreen },
})

export default createAppContainer(TabNavigator)
```

다음과 같이 실행됩니다.

![](/assets/img/posts/2019-08-03-18-39-09.png)