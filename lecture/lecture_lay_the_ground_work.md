## 🧐 Webpack에 대해 좀 더 자세히 알아보자.. 
> Webpack 👉 module bundler (여러 파일들을 하나로 묶어주는 기능)

### Vue에서 Webpack이 필요한 이유??
- `Single File Component` 컨셉으로 개발할 경우 하나의 `.vue`파일에 `HTML`/`CSS`/`JavaScript`를 모두 기술하게 됨
- 이렇게 작성한 `.vue` 파일은 브라우저가 인식할 수 없음
- `loader`와 `plugin` 등을 사용하여 .vue 파일을 컴파일하고 번들링하는 작업이 필요함

### 실습을 위한 기본 설정
  ```bash
  mkdir webpack-demo-app
  cd webpack-demo-app

  # package.json 파일 만들기
  npm init -y
  
  # webpack, vue 설치
  npm install -D webpack webpack-cli
  npm install vue
  ```
### package.json 수정
```diff
"scripts": {
+   "build": "webpack",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```

### `webpack.config.js` 파일 생성
```js
const path = require('path')

module.exports = {
  entry: {
    app: path.join(__dirname, 'index.js')
  },
  module: {
    rules: [],
  },
  plugins: [],
  output: {
    path: path.join(__dirname, 'dist'),
    filename: 'build.js'
  },
};
```


### `index.html`, `index.js` 파일 생성
index.html
```html
<html>
  <head>
    <title>webpack demo app</title>
  </head>
  <body>
    <div id="app"></div>
    <script src="./dist/build.js"></script>
  </body>
</html>
```

index.js
```js
import Vue from 'vue'

new Vue().$mount('#app')
```

### webpack 실행
```bash
npm run build
```