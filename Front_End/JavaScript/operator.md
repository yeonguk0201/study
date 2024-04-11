### 연산자

 <br>

- 표현식  <br>
  표현식이란 리터럴, 식별자, 연산자, 함수 호출 등의 조합을 말한다.

```javascript
//리터럴 표현식
10;

// 식별자 표현식
sum;

// 연산자 표현식
10 + 20;

// 함수&메소드 호출 표현식
square();
```

 <br>

- 산술 연산자  <br>
- 단항 산술 연산자  <br>
  ++와 -- 연산자가 있는데 앞 뒤에 따라 다르다.

  ```javascript
  let x = 5,
    result;

  // 선대입 후증가
  result = x++;
  console.log(result, x); // 5 6

  // 선증가 후대입
  result = ++x;
  console.log(result, x); // 7 7
  ```

  이렇게 앞에 있으면 먼저 증가하고 뒤에 있으면 뒤에 증가한다.
