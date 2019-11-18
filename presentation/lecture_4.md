---
marp: true
---
<style>
::-webkit-scrollbar { width: 8px; } 
::-webkit-scrollbar-thumb { background: #a9a9a9; }
.scroll {overflow-y:scroll;margin-bottom:20px;}
.center-image{display: block; margin-left: auto; margin-right: auto;}
img{margin-bottom:20px;}
table {font-size: 25px}
</style>

# Vue CLI

---

- Vue.js 개발 환경을 빠르고 쉽게 제공
- 공식 지원되는 도구
- `project scffoding` 제공 (👉 프로젝트 폴더 구조 및 라이브러리 설정)
- Vue CLI를 쓰지 않고 직접 설정도 가능하지만 추천 ❌  

> <del>현재 `v4.0.0-rc.7` 까지 Pre-release 된 상태이지만 `3.x` version을 사용할 예정입니다.</del>

> 게으른 탓인지 글을 쓰는 중에 `4.x` version이 공식 릴리즈 되었습니다 😅 
> `4.x` version 을 사용해야 할 것 같습니다 ㅎ

---

# Vue CLI 구성요소

---

## CLI

- `vue` 명령어 제공

---

  |command|desc|
  |-|-|
  |**create** [options] <app-name> |프로젝트 생성|
  |**add** [options] <plugin> [pluginOptions]|`npm install ` + 이미 생성된 프로젝트에 plugin 추가|
  |**invoke** [options] <plugin> [pluginOptions]|이미 생성된 프로젝트에 plugin 추가|
  |**inspect** [options] [paths...]|프로젝트의 webpack 설정 파일 자세히 보기|
  |**serve** [options] [entry]|개발 모드로 Application 실행 <br/>@vue/cli-service-global 전역 설치 필수|
  |**build** [options] [entry]|운영 모드로 Application 빌드 <br/>@vue/cli-service-global 전역 설치 필수|
  |**ui** [options]|vue-cli ui 시작하기|
  |**init** [options] \<template> \<app-name>|다른 Template으로 프로젝트 생성 <br/> (legacy API, @vue/cli-init 설치 필수)|
  |**config** [options] [value]|설정 자세히 보기 및 수정|
  |**upgrade** [semverLevel] | vue cli service / plugins 업그레이드 <br/>(default semverLevel: minor)|
  |**info**|디버깅 정보 출력|

---

## CLI Service

- 복잡한 `webpack` 설정을 알아서 해줌 
- `webpack-dev-server` 를 사용하여 Hot Module Replacement 가 가능하도록 함  
  (👉 코드를 저장하면 브라우저에 바로 반영)
- 사용 가능한 명령어는 `package.json` 에 정의되어 있음

---

  |command|desc|
  |-|-|
  |serve|개발서버 시작|
  |build|배포를 위한 빌드|
  |inspect|웹팩 내부 설정 보기|
  |lint|소스코드 작성 규칙 검사 및 수정|

> react의 `react-scripts` 와 유사한 개념  
> 참고자료 : [What exactly is the 'react-scripts start' command?](https://stackoverflow.com/questions/50722133/what-exactly-is-the-react-scripts-start-command)

---

## Vue CLI 설치
```bash
$> npm i -g @vue/cli
```

> Mac OS 사용 시 앞에 `sudo` 붙여야 함

<br/>

```bash
$> vue -V
3.11.0
```

> 😎 `lecture_1` 에서 설치했다면 Pass 하셔도 됩니다.

---

# Vue.js 로 SPA 만들기
## Project 만들기
```bash
$> vue create shoppingmall
```
---

<iframe src="https://player.vimeo.com/video/367217922" width="100%" height="100%" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

---

> `vue-cli 2.X` 에서는 `vue init <template-name> <project-name>` 명령어를 통해 프로젝트를 생성했었습니다.   
>
>관련된 내용은 [vue-cli v2 github](https://github.com/vuejs/vue-cli/tree/v2#vue-cli--) 를 참고하시기 바랍니다.

---

### preset 수동 설정하기

---

- 추가적인 설정을 해줘야 하기 때문에 `Manually select features` 선택
  <img src="./images/lecture_4/make-project-1.png" />

---

- `Router`, `Vuex` 추가  
(실제 개발 시 필수 선택 항목)
  <img src="./images/lecture_4/make-project-2.png" />

---

- `history mode` 사용  
  (`vue-router`의 기본 모드는 `hash mode`임)
  <img src="./images/lecture_4/make-project-3.png" />

---

- linter / formatter 는 `ESLint + Prettier`로 설정
  <img src="./images/lecture_4/make-project-4.png" />

---

- 추가적인 lint 설정  
(파일 저장 시 규칙에 맞게 코드가 작성되었는지 체크)
  <img src="./images/lecture_4/make-project-5.png" />

---

- Babel, PostCSS, ESLint 등의 설정 파일은 전용 설정 파일 생성
  <img src="./images/lecture_4/make-project-6.png" />

---

- 이렇게 프로젝트 설정한 값들을 저장할 수 있지만 여기서는 N 선택
  <img src="./images/lecture_4/make-project-7.png" />

---

- 프로젝트 생성 완료
  <img src="./images/lecture_4/make-project-8.png" />

---

## 실행하기

---

- `npm run serve` 실행  
(만약에 8080 포트가 사용 중이라면 다른 포트 번호로 실행될 수 있음)
  <img src="./images/lecture_4/make-project-9.png" />
---

- 브라우저에서 `http://localhost:8080` 접속
<img src="./images/lecture_4/make-project-10.png" width="800px" />

---

## 스캐폴딩 된 소스코드 구조 분석
<img src="./images/lecture_4/1.png" width=300px />

---

1. 📂**node_modules** : 프로젝트를 빌드하는 데 필요한 모든 라이브러리가 저장되는 곳  
(`npm install` 명령어를 실행하면 폴더가 생성됨)

2. 📂**public** : Webpack을 통해 관리되지 않는 정적 Resource들을 모아두는 곳.
    > ⚠️ image나 font 같은 정적 Resource들은 **src/assets** 폴더에 넣어서 Webpack의 관리를 받게하는 것을 추천

---

3. 📂**src/components** : 어플리케이션에서 사용되는 컴포넌트들을 모아두는 곳

4. 📂**src/router** : Router 설정 파일들을 모아두는 곳 (Client-Side-Routing)

5. 📂**src/store** : Vuex 설정 파일들을 모아두는 곳 (State 관리)

6. 📂**src/views** : Application의 다른 뷰 또는 페이지에 대한 파일을 저장하는 위치

---

7. 📄**App.vue** : 다른 컴포넌트를 포함하고 있는 최상위(root) 컴포넌트

8. 📄**main.js** : 어플리케이션에 필요한 요소들을 Load하여 렌더링한 후 DOM에 마운트하게 하는 작업 수행
    ```js
    import Vue from "vue";
    import App from "./App.vue";
    import router from "./router";
    import store from "./store";

    Vue.config.productionTip = false;

    new Vue({
      router,
      store,
      render: h => h(App)
    }).$mount("#app");
    ```
---

9. 📄**package.json** : 프로젝트에 필요한 package 들을 정의하고 관리해줌

> ✔️. 프로젝트 생성시 Babel, PostCSS, ESLint 등의 설정 파일은 전용 설정 파일 생성하도록 선택하였기 때문에  `.eslintrc.js`, `babel.config.js`, `postcss.config.js` 파일이 생성됨

---

## Beautify with Vuetify
Vuetify = Vue + Design System(Material Design)

---

### Add Vuetify Plugin 
```bash
$> vue add vuetify
```

---

## 참고자료
[Vue CLI](https://cli.vuejs.org/)  
[[Vue] 개발환경 만들기 (without vue-cli)](https://velog.io/@kyusung/Vue-app-sfc-without-vue-cli)  
[Vue CLI 3.X 사용하기](https://velog.io/@skyepodium/Vue-CLI-3.X-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)