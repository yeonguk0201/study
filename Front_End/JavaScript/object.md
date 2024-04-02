### 객체 리터럴

1. 객체란?
   자바스크립트는 객체 기반 프로그래밍 언어로 거의 모든 것이 객체다.
   원시 값은 변경 불가능한 값이지만 객체는 변경 가능한 값으로 객체는 0개 이상의 프로퍼티로 구성된 집합이며, 프로퍼티는 키와 값으로 구성된다.

```javascript
let person = {
  name: 'Lee',
  age: 20,
};
// 2개의 프로퍼티가 키와 값으로 구성된다.
```

자바스크립트에서 사용할 수 있는 모든 값은 프로퍼티 값이 될 수 있다. 함수는 일급 객체이므로 값으로 취급 가능한데, 이 경우 메서드라고 부른다.
그래서 객체는 프로퍼티와 메서드로 구성된 집합체로 프로퍼티는 객체의 상태를 나타내고 메서드는 프로퍼티를 참조하고 조작할 수 있는 동작이다.

  <br>

2. 객체 리터럴에 의한 객체 생성
   C++나 자바 같은 클래스 기반 객체지향 언어는 클래스를 사전에 정의하고 필요한 시점에 new 연산자와 함께 생성자를 호출해 인스턴스를 생성하는 방식으로 객체를 생성한다.
   > > 인스턴스란 클래스에 의해 생성되어 메모리에 저장된 실체를 말한다. 객체지향 프로그래밍에선 객체는 클래스와 인스턴스를 포함한 개념이다. 인스턴스는 객체가 메모리에 저장되어 실제로 존재하는 것에 초점을 맞춘 용어다.

  <br>
  자바스크립트는 프로토타입 기반 객체지향 언어로서 다양한 객체 생성 방법을 지원한다.
  - 객체 리터럴
  - Object 생성자 함수
  - 생성자 함수
  - Object.create 메서드
  - 클래스

가장 간단한 것은 위의 예제처럼 객체 리터럴을 사용하는 방법으로 중괄호 써서 만드는 방법이다.
객체 리터럴의 중괄호는 코드 블록을 의미하지 않는다.
<br>

3. 프로퍼티
   프로퍼티를 나열할 때는 쉼표(,)로 구분한다.
   프로퍼티 키는 식별자 네이밍 규칙을 무조건 따라야 하지는 않지만, 따르지 않으면 따옴표를 사용해서 적어야 한다.

```javascript
let person = {
  firstName: 'Ung mo',
  'last-name': 'Lee',
  second-name: 'Gee'
};
```

이렇게 따옴표를 생략하면 -연산자가 있는 표현식으로 해석한다.
<br>
문자열 또는 문자열로 평가할 수 있는 표현식을 사용해 키르 동적으로 생성할 수 있다. 이 경우 대괄호[]를 사용해야 한다.

```javascript
let obj = {};
let key = 'hello';
obj[key] = 'world';
console.log(obj); // {hello: 'world'}
```

또 프로퍼티 키에 문자열이나 심벌 값 외의 값을 사용하면 암묵적으로 문자열로 변환된다. 그리고 키를 중복 선언하면 나중에 선언한 프로퍼티가 된다.

```javascript
let foo = {
  0: 1,
  1: 2,
  name: 'Lee',
  name: 'Kim',
};

console.log(foo); // {0: 1, 1: 2, name: 'Kim'}
```

<br>

4. 메서드
   프로퍼티 값이 함수면 일반 함수와 구분하기 위해 메서드라 부른다.

```javascript
let circle = {
  radius: 5,
  getDiameter: function () {
    return 2 * this.radius;
  },
};

console.log(circle.getDiameter()); //10
```

메서드 내부에서 사용한 `this`는 객체 자신을 가리키는 참조변수다.
<br>

5. 프로퍼티 접근
   접근하는 방식은 두 가지다.

- 마침표 표기법
- 대괄호 표기법
  프로퍼티 키가 식별자 네이밍을 준수하는 이름이면 둘 다 사용할 수 있다.

```javascript
let person = {
  name: 'Lee',
  'last-name': 'Kim',
  1: 10
};

console.log(person.name); // Lee
console.log(person['name']); // Lee
console.log(person.last-name); // NaN     person.last를 평가하고 거기서 -name으로 되서 이렇게 나온다.
console.log(person['last-name']); // Kim
console.log(person.1); //SyntaxError
console.log(person[1]); //10 : person['1']로 바뀐다.
console.log(person['1']); //10
```

이처럼 대괄호 표기법을 사용하는 경우 키는 반드시 따옴표로 감싼 문자열이어야 한다.

<br>

6. 프로퍼티 값 갱신

```javascript
let person = {
  name: 'Lee',
};

person.name = 'Kim';
console.log(person); //{name: 'Kim'}
```

<br>

7. 프로퍼티 동적 생성

```javascript
let person = {
  name: 'Lee',
};

person.age = 20;
console.log(person); //{name: 'Kim', age: 20}
```

<br>

8. 프로퍼티 삭제
   delete를 사용하면 삭제가 가능하다.

```javascript
let person = {
  name: 'Lee',
  age: 20,
};

delete person.age;
console.log(person); //{name: 'Kim'}
```

<br>

9. ES6에서 추가된 객체 리터럴 확장 기능

   - 변수 이름과 프로퍼티 키가 동일하면 키를 생략할 수 있다.

   ```javascript
   let x = 1,
     y = 2;
   const obj = { x, y };
   console.log(obj); // {x: 1, y: 2}
   ```

- 계산된 프로퍼티 이름
  문자열 또는 문자열로 타입 변환할 수 있는 값으로 평가되는 표현식을 사용해 키를 생성할 수 있는데 대괄호로 묶어야 한다.

```javascript
const prefix = 'prop';
let i = 0;

const obj = {
  [`${prefix} - ${++i}`]: i,
  [`${prefix} - ${++i}`]: i,
  [`${prefix} - ${++i}`]: i,
};

console.log(obj); // {prop-1: 1, prop-2: 2, prop-3: 3}
```

- 메서드 축약 표현
  ES6에선 function 키워드 생략해서 사용할 수 있다.

```javascript
const obj = {
  name: 'Lee',
  sayHi() {
    console.log('Hi! ' + this.name);
  },
};

obj.sayHi(); // Hi! Lee
```

근데 ES5는 function 키워드 넣어야 한다.

```
sayHi: function(){

}
```

이렇게
