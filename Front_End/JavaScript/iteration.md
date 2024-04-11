### 이터레이션

---

이터레이션이란 프로토콜은 ES6에서 도입되었으며 데이터 컬렉션을 순회하기 위한 프로토콜이다.
for-of문으로 순회할 수 있다.

- 이터러블  <br>
  위 프로토콜을 준수한 객체를 이터러블이라고 한다. 이터러블은 Symbol.iterator 메소드를 구현하거나 프로토타입 체인에 의해 상속한 객체를 말한다.
  배열은 Symbol.iterator 메소드를 소유해서 배열은 이터러블이다.

</br>

하지만 일반 객체는 이터러블이 아니다. 그래서 순회가 불가하다.

```javascript
const array = [1, 2, 3];
console.log(Symbol.iterator in array); //true
```

이렇게 확인해 볼 수 있다. 배열 같은 건 Symbol.iterator 메소드를 가지고 있어서 true라고 나온다.

</br>

- 이터레이터  <br>
  이터레이터 프로토콜은 next 메소드를 가지며 호출하면 이터러블을 순회하면서 value, done 프로퍼티를 갖는 객체를 반환한다.
  그러니까 이터레이터 프로토콜을 준수한 이터레이터는 next 메소드를 가진다.

```javascript
// 배열은 이터러블 프로토콜을 준수한 이터러블이다.
const array = [1, 2, 3];

// Symbol.iterator 메소드는 이터레이터를 반환한다.
const iterator = array[Symbol.iterator]();

// 이터레이터 프로토콜을 준수한 이터레이터는 next 메소드를 갖는다.
console.log('next' in iterator); // true
```

※ `array[Symbol.iterator]()` 이 부분! 이 부분은 대괄호 표기법을 사용해 Symbol.iterator을 호출한 것으로 Symbol.iterator가 메소드니까 ()로 바로 실행했다.

</br>

이제 next를 호출하면 value, done 프로퍼티를 갖는 iterator result 객체를 반환한다.

```javascript
let iteratorResult = iterator.next();
console.log(iteratorResult); // {value: 1, done: false}
```

</br>

value는 값, done은 마지막인지 확인한다.

```javascript
const array = [1, 2, 3];

const iterator = array[Symbol.iterator]();

console.log('next' in iterator); // true

// next 메소드를 호출할 때 마다 이터러블을 순회하며 이터레이터 리절트 객체를 반환한다.
console.log(iterator.next()); // {value: 1, done: false}
console.log(iterator.next()); // {value: 2, done: false}
console.log(iterator.next()); // {value: 3, done: false}
console.log(iterator.next()); // {value: undefined, done: true}
```

</br>

ES6에서 제공하는 빌트인 이터러블은 다음과 같다.

> > Array, String, Map, Set, TypedArray(Int8Array, Uint8Array, Uint8ClampedArray, Int16Array, Uint16Array, Int32Array, Uint32Array, Float32Array, Float64Array), DOM data structure(NodeList, HTMLCollection), Arguments

- Map  <br>
  키-값 쌍으로 이루어진 자료구조다. 중복된 키를 허용하지 않으며 순서가 정의되어 있지 않다.

  ```javascript
  const myMap = new Map();

  // 값 추가
  myMap.set('key1', 'value1');
  myMap.set('key2', 'value2');
  myMap.set('key3', 'value3');

  // 값 조회
  console.log(myMap.get('key2')); // 'value2'

  // 값 존재 여부 확인
  console.log(myMap.has('key3')); // true
  console.log(myMap.has('key4')); // false

  // 값 삭제
  myMap.delete('key1');

  // 맵 크기 확인
  console.log(myMap.size); // 2

  // 전체 값 순회
  for (let [key, value] of myMap) {
    console.log(`${key}: ${value}`);
  }
  ```

- Set  <br>
  Set은 중복을 허용하지 않는 값들의 집합을 나타내는 자료구조로 순서는 정의되어 있지 않고 값의 고유성을 보장한다.

  ```javascript
  const mySet = new Set();

  // 값 추가
  mySet.add(1);
  mySet.add(2);
  mySet.add(3);
  mySet.add(1); // 중복된 값은 추가되지 않음

  // 값 존재 여부 확인
  console.log(mySet.has(2)); // true
  console.log(mySet.has(4)); // false

  // 값 삭제
  mySet.delete(2);

  // 셋 크기 확인
  console.log(mySet.size); // 2

  // 전체 값 순회
  for (let item of mySet) {
    console.log(item);
  }
  ```

  </br>

  - Arguments  <br>
    인자는 함수 내부에서 사용되는 객체로 함수가 호출될 때 전달되는 인자들의 목록을 나타낸다.
    배열과 유사하게 인덱스로 접근 가능하지만, 배열이 아닌 유사 배열 객체이다.

  함수 내부에서 arguments 키워드를 통해 접근할 수 있다.

  ```javascript
  function myFunction() {
    console.log(arguments.length); // 전달된 인자의 개수 출력
    console.log(arguments[0]); // 첫 번째 인자 출력
  }

  myFunction(1, 2, 3); // 3, 1 출력
  ```

  유사 배열 객체이기 때문에 배열 메서드를 직접 사용할 수는 없지만 인덱스를 통해 접근할 수는 있다.
  배열로 바꾸고 싶다면 Array.from() 메서드나 스프레드 문법 등으로 변환할 수 있다.
