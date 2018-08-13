---
layout: post
title: Electron 프로젝트에서 Realm 사용하기
categories: [공부이야기, Electron]
tags: [electron, java script, desktop app]
fullview: true
comments: true
---
# Electron 프로젝트에서 Realm 사용하기
## 1. electron-rebuild
`npm install —save realm`
을 입력해서 프로젝트에 realm-js를 설치한다.
하지만 이 상태에서 import 하면 can’t find module 에러가 뜬다.

`electron-rebuild` 를 사용하면 이 문제를 해결 가능한데
`npm install —save-dev electron-rebuild` 로 모듈을 설치하고
`package.json` 에 script 항목에
`“rebuild : “electron rebuild -f -w realm”` 를 추가한 후

```sh
npm run rebuild
```

를 실행하면 정상적으로 Main Process, Renderer Process 모두에서 import 가능하다.

## Vuex 를 포기
Vue.js 를 프론트앤드 프레임워크로 선정한 후에 Vuex도 같이 적용하기로 한 이유가 단방향 데이터 흐름을 가진 스토어 구축이었는데, Vuex의 Action, Mutation, Store 등의 개념을 Electron의 Main Process / Renderer Process 에 적용시켜서 생각하려니 여간 복잡한게 아니었다. 그러던 중, [Bringing Native Performance to Electron](https://realm.io/blog/native-performance-electron-realm/) 을 읽고 Vuex를 과감하게 포기하기로 했다.
이 포스팅에서는 Realm 에서 제공하는 Notification 기능과 Electron의 Main/Renderer Process 만으로도 충분히 단방향의 데이터 흐름을 만들 수 있다는 것을 설명하고 있다.
![](&&&SFLOCALFILEPATH&&&realm+electron.png)
