# 진짜 Vue.js 개발 시작하기

# Vue CLI
**Vue.js 개발을 위한 환경을 빠르고 쉽게 제공함**
- 스캐폴딩(Scffoding) 코드 제공
- 복잡한 Webpack 설정을 알아서 해줌 
- `webpack-dev-server` 를 사용하여 Hot Module Replacement 가 가능하도록 함  
  (👉 코드를 저장하면 브라우저에 바로 반영)


## Install CLI
```bash
npm i -g @vue/cli
```
> 😎 `lecture_1` 에서 설치했다면 Pass

## Create Project
```bash
vue create real-vue-project
```

## Webpack
Webpack 👉 module bundler
여러 파일을 하나로 묶어주는 기능

.vue 파일은 브라우저가 인식할 수 없음
loader와 plugin을 사용하여 html, css, js로 변환

vue 단일 파일 컴포넌트를 사용하기 위해서는 .vue 파일을 컴파일하고 번들링하는 작업이 필요합니다.


# Vue Router

# Vue Components

# API 호출 (with. Axios)

## 참고자료
[[Vue] 개발환경 만들기 (without vue-cli)](https://velog.io/@kyusung/Vue-app-sfc-without-vue-cli)