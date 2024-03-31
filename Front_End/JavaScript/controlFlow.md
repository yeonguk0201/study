### 제어문

1. 블록문
   블록문은 0개 이상의 문들을 묶은 것으로 코드 블록 또는 블록이라고 부른다.

```javascript
{
  var foo = 10;
  console.log(foo);
}
```

<br>

2. 조건문

- if..else 문

```javascript
if (조건식) {
  // 조건식이 참이면 이 코드 블록이 실행된다.
} else {
  // 조건식이 거짓이면 이 코드 블록이 실행된다.
}
```

만약 블록 내의 문이 하나라면 중괄호 생략 가능하다.

```javascript
let num = 2;
let kind;

if (num > 0) kind = '양수';
else if (num < 0) kind = '음수';
else kind = '영';
```

당연히 삼항 조건 연산자로 바꿔쓸 수 있다.

  <br>

- switch 문

```javascript
switch (표현식) {
  case 표현식1:
    switch 문의 표현식과 표현식1이 일치하면 실행될 문;
    break;
  case 표현식2:
    switch 문의 표현식과 표현식2가 일치하면 실행될 문;
    break;
  default:
    switch 문의 표현식과 일치하는 표현식을 갖는 case 문이 없을 때 실행될 문;
}
```

일치하는 case가 없으면 default 문으로 이동한다. default는 옵션이다.
break문을 꼭 넣어야지 코드 블록에서 탈출할 수 있다. defalut 문에는 일반적으로 break를 생략한다.
여러 개의 case 문을 중복해서 사용할 수 있다.

```javascript
let year = 2000;
let month = 2;
let days = 0;

switch (month) {
  case 1:
  case 3:
  case 5:
  case 7:
  case 8:
  case 10:
  case 12:
    days = 31;
    break;
  case 4:
  case 6:
  case 9:
  case 11:
    days = 30;
    break;
  case 2:
    // 윤년 계산 알고리즘
    // 1. 년도가 4로 나누어 떨어지는 해는 윤년(2000, 2004, 2008, 2012, 2016, 2020…)
    // 2. 그 중에서 년도가 100으로 나누어 떨어지는 해는 평년(2000, 2100, 2200...)
    // 3. 그 중에서 년도가 400으로 나누어 떨어지는 해는 윤년(2000, 2400, 2800...)
    days = (year % 4 === 0 && year % 100 !== 0) || year % 400 === 0 ? 29 : 28;
    break;
  default:
    console.log('Invalid month');
}
```

<br>

3. 반복문

- for 문
  조건식이 거짓을 판별될 때까지 반복한다.
- while 문
  조건식이 참이면 실행한다.
- do...while 문
  일단 실행하고 조건식을 평가하고 다시 실행한다.
  <br>

4. break 문

```javascript
// 문자열은 유사배열이므로 for 문으로 순회할 수 있다.
for (var i = 0; i < string.length; i++) {
  // 문자열의 개별 문자가 'l'이면
  if (string[i] === 'l') {
    index = i;
    break; // 반복문을 탈출한다.
  }
}
```

아래 예제처럼 활용 가능하다. 순회하는 횟수를 줄여줌으로서 연산양을 줄였다.

```javascript
for (var i = 0; i < 10; i++) {
  if (i == 5) {
    // i 가 5 와 같을 경우
    break; // for 문 종료
  }
  console.log(i); // 0,1,2,3,4
}
```

```javascript
for (var i = 0; i < 10; i++) {
  if (i < 5) {
    // i 가 5 보다 작을 경우
    console.log(i); // 0,1,2,3,4
  }
}
```

break문은 6번 if문은 10번 순환했다.
<br>

5. continue 문
   현재 순환부를 종료하고 다음 순환으로 넘어간다.
