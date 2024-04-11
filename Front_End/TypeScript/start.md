### 타입 스크립트란?

- 타입스크립트는 자바스크립트에 타입을 부여한 언어로 컴파일 과정을 거친다.
  타입을 부여함으로써 에러를 사전에 방지하고 vscode의 내부가 타입스크립트로 작성되어 있어서 타입스크립트 개발에 좋다.

<br>

1. 에러 방지 예제

```javascript
//math.js
function sum(a, b) {
  return a + b;
}

//math.ts
function sum(a: number, b: number) {
  return a + b;
}
```

이렇게 하면 만약 a와 b에 숫자가 아닌 문자열이 들어가는 등의 에러를 사전에 방지할 수 있다.
