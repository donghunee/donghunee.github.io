---
layout: post
title: '[Git].gitignore 적용안될 때 해결 방법'
subtitle: '.gitignore 적용안될 때 해결 방법'
categories: 'study'
tags: 'etc'
---


까끔식 gitignore가 적용이 안되는 문제가 생길때가 있다. 이때 해결방법을 기록해보았습니다.!!

```
$ git rm -r --cached .
$ git add .
$ git commit -m "fixed untracked files”
```
