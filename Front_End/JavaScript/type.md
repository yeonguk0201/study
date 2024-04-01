### 타입 변환과 단축 평가

1. 타입 변환이란?
   타입 변환엔 2가지가 있는데 하나는 의도적으로 바꾸는 **명시적 타입 변환** 또는 **타입 캐스팅**, 그리고 자바스크립트 엔진에 의해 암묵적으로 변경되는 **암묵적 타입 변환** 또는 **타입 강제 변환**이 있다.

<br>
명시적 타입 변환은 .toString() 등을 사용하여 타입을 바꾸는 것이고 암묵적 타입 변환은 숫자를 문자열과 합쳐서 문자열로 만드는 등의 그런 방식이다.

```javascript
// 명시적
let x = 10;
let str = 10.toString();

// 암묵적
let ssttrr = 10 + '';
```

이렇게 명시적은 명백히 드러나는 반면 암묵적은 그렇지 않다. 그렇다면 무조건 명시적 표현이 좋은 것일까??
꼭 그런 것은 아니다. 10.toString() 보다 10 + ''이 더욱 간결하고 이해하기 쉬울 수 있기 때문이다.

- 암묵적 타입 변환

  - 문자열 타입으로 변환
    템플릿 리터럴도 암묵적 변환이다.

    ```javascript
    `1 + 1 = ${1 + 1}`;
    ```

  - 숫자 타입으로 변환
    `+`는 문자열 연결 연산자로 작동된다. 하지만 다른 산술 연산자는 문자열이 있어도 숫자로 변환한다.

    ```javascript
    1 - '1'; // 0
    1 * '10'; // 10
    1 / 'one'; // NaN
    ```

    비교 연산자의 역할은 불리언 값을 만드는 것으로 숫자 타입이 아닌 피연산자를 숫자 타입으로 암묵적 타입 변환한다.

    - 연산자는 피연산자가 숫자 타입의 값이 아니면 숫자 타입의 값으로 암묵적 타입 변환한다.

    ```javascript
    '1' >
      0 + // true
        '' + // 0
        '0' + // 0
        '1' + // 1
        'string' + // NaN
        true + // 1
        false + // 0
        null + // 0
        undefined + // NaN
        Symbol() + // TypeError: Cannot convert a Symbol value to a number
        {} + // NaN
        [] + // 0
        [10, 20] + // NaN
        function () {}; // NaN
    ```

    이렇게 빈 문자열, 빈 배열, null, false는 0으로, true는 1로 변환된다.
    객체와 빈 배열이 아닌 배열, undefined는 변환되지 않아서 NaN으로 된다.

  - 불리언 타입으로 변환
    자바스크립트 엔진은 불리언 타입이 아닌 값을 Truthy 또는 Falsy값으로 구분한다.
    falsy값은
    - false
    - undefined
    - null
    - 0, -0
    - NaN
    - '' (빈문자열)

<br>

- 명시적 타입 변환
  - 문자열 변환
    1. String() 생성자 함수
    2. .toString()
    3. 문자열 연결 연산자 이용
    ```javascript
    console.log(String(1)); // "1"
    console.log(NaN.toString()); // "NaN"
    console.log(Infinity + ''); // "Infinity"
    ```
  - 숫자로 변환
    1. Number() 생성자 함수
    2. parseInt, parseFloat
    3. 단항 연결, 산술 연산자 사용
    ```javascript
    console.log(Number('0')); // 0
    console.log(parseFloat('10.53')); // 10.53
    console.log(+false); // 0
    console.log(true * 1); // 1
    console.log('-1' * 1); // -1
    ```
  - 불리언 타입으로 변환
    1. Boolean() 생성자 함수
    2. !부정 논리 연산자 두 번 사용
    ```javascript
    console.log(Boolean('')); // false
    console.log(Boolean('false')); // true
    console.log(Boolean('x')); // true
    console.log(Boolean('')); // false
    console.log(Boolean('false')); // true
    ```

근데 여기 +연산자가 명시에도 나오고 암묵에도 나오는데 내 생각엔 암묵적 변환을 명시적으로 활용함으로서 명시적이라고 한 것 같다.

<br>
<br>

2. 단축 평가

- 논리 연산자를 사용한 단축 평가
  논리합 || 또는 논리곱 &&의 평가 결과는 불리언 값이 아닐 수 있다. 언제나 2개의 피연산자 중 어느 한쪽으로 평가된다.

  ```javascript
  'Cat' && 'Dog'; // "Dog"
  'Cat' || 'Dog'; // "Cag"
  ```

  이렇게 논리곱 연산자는 좌에서 우로 진행되고 두 개 모두 true로 평가되야 true를 반환한다.
  'Cat'은 Truthy 값으로 true로 평가되기 때문에 true && 'DOG 이렇게 돼서 'Dog'를 반환한다.
  논리합 연산자도 좌에서 우로 평가되지만 두 개중 하나만 true여도 true를 반환하니까 'Cat'을 반환한다.
  이처럼 논리 연산의 결과를 결정하는 피연산자를 타입 변환하지 않고 그대로 반환하는 것을 **단축 평가**라고 한다.

  ```javascript
  // 논리합(||) 연산자
  'Cat' || 'Dog'; // 'Cat'
  false || 'Dog'; // 'Dog'
  'Cat' || false; // 'Cat'

  // 논리곱(&&) 연산자
  'Cat' && 'Dog'; // Dog
  false && 'Dog'; // false
  'Cat' && false; // false
  ```

  단축 평가로 if문을 대체할 수 있다.

  ```javascript
  let done = true;
  let message = '';

  // 주어진 조건이 true
  if (done) message = '완료';

  // if 문은 단축 평가로 대체 가능하다.
  message = done && '완료';

  let none = false;
  if (!none) message = '미완료';

  // 논리합 연산자로 대체 가능
  message = done || '미완료';
  ```

  꽤 유용하게 많이 쓰이는 방법이라 자주 써서 익히면 좋다.

  ##### 객체를 가리키기를 기대하는 변수가 null 또는 undefined가 아닌지 확인하고 프로퍼티를 참조할 때

  객체는 키와 값으로 구성된 프로퍼티의 집합이다. 객체를 가리키기를 기대하는 변수가 객체가 아니면 에러가 발생하는데 단축 평가를 사용하면 에러가 나지 않는다.

  ```javascript
  let elem = null;
  let value = elem.value; // TypeError

  let realValue = elem && elem.value; // null
  ```

- 옵셔널 체이닝 연산자
  옵셔널 체이닝 연산자는 ES11에 도입된 것으로 `?.`로 좌항의 피연산자가 null 또는 undefined인 경우 undefined를 반환하고 그렇지 않으면 우항의 프로퍼티 참조를 이어간다.
  도입되기 전에는 &&를 썼다.

  ```javascript
  let elem = null;
  let value = elem?.value;
  console.log(value); // undefined

  let vv = elem && elem.value;
  console.log(value); // null
  ```

  차이점은 &&는 좌항이 false면 좌항 연산자를 반환한다.
  하지만 옵셔널 체이닝 연산자는 좌항이 false여도 null이나 undefined가 아니면 우항의 프로퍼티 참조를 이어간다.

  ```javascript
  let str = '';
  let length = str && str.length;
  console.log(length); // ''

  // 옵셔널 체이닝의 경우
  let length = str?.length;
  console.log(length); // 0
  ```

  <br>

- null 병합 연산자
  ES11에서 도입된 null 병합 연산자 ??는 좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환하고 아니면 좌항을 반환한다.
  변수에 기본값을 설정할 때 유용하다.
  도입되기 이전엔 ||를 사용했다.

  ```javascript
  let foo = null ?? 'default';
  console.log(foo); // 'default'

  // ||의 경우
  let foo = '' || 'default';
  console.log(foo); // default
  ```

  하지만 null 병합 연산자는 좌항이 false라도 null이나 undefined가 아니면 좌항을 그대로 반환한다.

  ```javascript
  let foo = '' ?? 'default';
  console.log(foo); // ''
  ```

null 병합 연산자랑 단축 평가는 많이 보여서 자주 써서 익혀보자!
