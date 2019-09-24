# Vue.js 반응 기법
- Vue 인스턴스가 초기화 될 때 data(javascript object)에 있는 모든 속성들에  `Object.defineProperty()` 메서드를 사용하여 getter/setter로 변환
- setter가 호출되면 내부 데이터를 변경하고 watcher에게 알림
- watcher는 Virtual DOM에 변경사항을 기록하고 re-render 를 명령함(비동기)
  ```js
  var obj = {
    data: {
      a: 100, b: 200, c: 300
    }
  };
  for (var k in obj.data) {
    (function (k) {
      Object.defineProperty(obj, k, {
        // obj에 값을 할당할 때 동작 정의
        set: function (x) {
          console.log("## setter call : ", k, x);
          this.data[k] = x;
          // watcher에게 알림~!!
        },
        // obj에 접근할 때 동작 정의
        get: function () {
          console.log("## getter call : ", k, this.data[k]); 
          return this.data[k];
        },
        enumerable: true, 
        configurable: true
      });
    })(k);
  }
  ```
> 이런 작업을 거쳐 data에 있는 속성들은 **반응(reactive) 속성**이 된다

<img src="./images/lecture_3/1.png" width="500">

## 인스턴스에 속성이 동적으로 추가된다면??
👉 이미 만들어진 인스턴스에 반응 속성을 동적으로 추가하는 것은 허용되지 않음
```js
var vm = new Vue({
  data: {
    a: 1
  }
})
// vm.a 는 반응적임
 
vm.b = 2
// vm.b 를 변경하면 화면변화 없음
```
> 하지만 이 경우에도 `Vue.set(object, key, value)` 메소드를 사용하여 변경사항을 감지하게 할 수 있다.

## 비동기 갱신 큐(Queue)
- 사용자가 데이터를 변경하면 watcher가 관리하는 Virtual DOM에는 즉시 반영되지만..
- DOM 조작을 최소화 하기 위해 모든 데이터 변경 사항은 버퍼링 됨  
  (버퍼링으로 중복이 제거된 작업)
- 버퍼링을 거쳐서 큐에 푸시가 되면 이벤트 루프 tick이 큐에 있는 내용을 비우면서 실제 DOM을 업데이트 함

## Vue는 DOM 업데이트를 비동기로 동작한다는데 문제는 없을까?
- Vue.nextTick() 
- this.$nextTick() -> Vue 인스턴스 내부에서




# Components
Components are reusable blocks of code that can have both structure and functionality. They help create a more modular and maintainable codebase.