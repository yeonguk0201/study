## 인터페이스

인터페이스는 보통 다음과 같은 범주에 대해 약속을 정의한다.

- 객체의 속성과 속성의 타입
- 함수의 파라미터, 반환 타입 등
- 배열과 객체를 접근하는 방식
- 클래스

### 인터페이스 맛보기

```typescript
let person = { name: 'Capt', age: 28 };

function logAge(obj: { age: number }) {
  // age를 가지고 있는 객체만을 인수로 받겠다는 뜻
  console.log(obj.age);
}
logAge(person); // 28
```

위 함수에서 받는 인자의 형태는 **age**를 속성으로 갖는 객체다. 이렇게 인자를 받을 때 타입 뿐만 아니라 객체의 속성 타입까지 정의할 수 있다.

그럼 여기에 **인터페이스**를 적용해보자.
<br>

```typescript
interface personAge {
  age: number;
}

function logAge(obj: personAge) {
  console.log(obj.age);
}

let person = { name: 'Capt', age: 28 };
logAge(person); // 28
```

이러면 `logAge()`의 인자가 좀 더 명시적으로 바뀌었다. 인자는 `personAge`라는 타입을 가져야 한다.

그리고 이렇게 인터페이스를 인자로 받아서 사용하면 꼭 인터페이스의 속성 갯수와 인자로 받는 객체의 속성 갯수를 일치시키지 않아도 된다. 즉, 인터페이스에 정의된 속성, 타입의 조건만 맞다면 객체의 속성 갯수가 더 많아도 상관 없다는 뜻이다.

### 옵션 속성

인터페이스를 사용할 때 인터페이스에 정의되어 있는 속성을 모두 사용하지 않아도 된다.

```typescript
interface 인터페이스_이름 {
  속성?: 타입;
}
```

꼭 보내지 않아도 되는 함수 인자를 쓸 때처럼 속성 끝에 `?`를 붙인다.

```typescript
interface CraftBeer {
  name: string;
  hop?: number;
}

let myBeer = {
  name: 'Saporo',
};

function brewBeer(beer: CraftBeer) {
  console.log(beer.name);
}

brewBeer(myBeer);
```
