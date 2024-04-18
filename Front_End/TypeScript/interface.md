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

이처럼 brewBeer()함수에서 CraftBeer 인터페이스를 인자의 타입으로 선언했지만 hop 속성이 없는 것 처럼 속성을 옵션으로 선언할 수 있다.

<br>

### 읽기 전용 속성

읽기 전용 속성은 인터페이스로 객체를 처음 생성할 때만 값을 할당하고 이후엔 변경할 수 없는 속성을 의미한다. 예제와 같이 `readonly`를 앞에 붙인다.

```typescript
interface CraftBeer {
  readonly brand: string;
}
```

인터페이스로 객체를 선언하고 나서 수정하려고 하면 이렇게 오류가 난다.

```typescript
let myBeer: CraftBeer = {
  brand: 'Belgian Monk',
};

myBeer.brand = 'Korean Carpenter'; // error!
```

이렇게 수정할 수 없다!

<br>

### 읽기 전용 배열

배열도 `ReadonlyArray<T>`로 타입을 사용하면 읽기 전용 배열을 생성할 수 있다.

```typescript
let arr: ReadonlyArray<number> = [1, 2, 3];
arr.splice(0, 1); // error
arr.push(4); // error
arr[0] = 100; // error
```

차이점은 속성은 속성 앞에 `readonly`를 붙이고 배열을 타입으로 선언한다. <br>

이렇게 할 수 도 있다.

```typescript
let arr: readonly number[] = [1, 2, 3];
```

<br>

### 객체 선언과 관련된 타입 채킹 (타입 단언)

```typescript
interface CraftBeer {
  brand?: string;
}

function brewBeer(beer: CraftBeer) {
  // ..
}
brewBeer({ brandon: 'what' }); // error: Object literal may only specify known properties, but 'brandon' does not exist in type 'CraftBeer'. Did you mean to write 'brand'?
```

위 코드를 보면 brandon에서 오류가 날 것이다. 왜냐면 인터페이스는 brand니까

만약 이런 타입 추론을 무시하고 싶다면 아래와 같이 선언한다.

```typescript
let myBeer = { brandon: 'what' };
brewBeer(myBeer as CraftBeer);
```

이렇게 `as`를 붙인다.
만약 인터페이스에서 정의하지 않은 속성을 추가로 사용하고 싶으면 아래처럼 한다.

```typescript
interface CraftBeer {
  brand?: string;
  [propName: string]: any;
}
```

타입 단언은 개발자가 해당 타입에 대해 확신이 있을 때 사용하는 타입 지정 방식이다.

아래 예시를 보자.

```typescript
interface human {
  sayhi: string;
  age: number;
}

let person = {};

person.sayhi = 'hi';
person.age = 32;
```

이러면 에러나는데 타입 단언을 사용해 보자.

```typescript
interface human {
  sayhi: string;
  age: number;
}

let person = {} as human;

person.sayhi = 'Hi';
person.age = 13;
```

물론 이렇게 해도 된다.

```typescript
interface human {
  sayhi: string;
  age: number;
}

let person = {
  sayhi: 'Hi',
  age: 13,
};
```

어쨌든 기존 코드에서 `as`만 써서 오류를 없앤다는 건데 아래처럼 타입 단언 후 아무것도 할당하지 않으면 런타입 환경에서 에러가 날 것이다.

```typescript
interface human {
  sayhi: string;
  age: number;
}

let person = {
  // 아무것도 안 넣음
} as human;

console.log(person.sayhi);
```

타입스크립트의 장점은 컴파일 단계에서 오류를 발견할 수 있는 장점이 있는데 런타임까지 가야 발견됐다는 것이 좋지 않다.

**그런데 왜 사용할까?**

적절하게 사용되는 예시 하나를 보면 **HTML 요소에 접근할 때**이다.
create-react-app으로 typescript react 앱 셋팅을 하면

```typescript
const container = document.getElementById('root') as HTMLDivElement;
const root = createRoot(container);

root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

이게 보이는데 여기 첫줄에 있다. <br>
`document.getElementById("root")` 를 변수에 할당하면 HTMLElement이거나 null 일 수 있다고 나오는데 프로젝트 특성상 HTMLDivElement인 걸 아니까 저렇게 작성돼있다.

<br>
보통 타입스크립트를 사용하면 `any`와 `타입 단언`은 피하라고 한다. <br>
하지만 '절대'가 아닌 '잘' 사용하면 된다!

<br>

### 함수 타입

인터페이스는 함수의 타입을 정의할 때도 사용한다.

```typescript
interface login {
  (username: string, password: string): boolean;
}
```

함수의 인자의 타입과 반환 값의 타입을 정할 수 있다.

```typescript
let loginUser: login;
loginUser = function (id: string, pw: string) {
  console.log('로그인');
  return true;
};
```

<br>

### 클래스 타입

클래스가 일정 조건을 만족하도록 타입 규칙을 정할 수 있다.

```typescript
interface CraftBeer {
  beerName: string;
  nameBeer(beer: string): void;
}

class myBeer implements CraftBeer {
  beerName: string = 'Baby Guiness';
  nameBeer(b: string) {
    this.beerName = b;
  }
  constructor() {}
}
```

<br>

### 인터페이스 확장

클래스처럼 인터페이스도 확장이 가능하다.

```typescript
interface Person {
  name: string;
}
interface Developer extends Person {
  skill: string;
}

let fe: Developer = {
  name: 'josh',
  skill: 'TypeScript',
};

// let fe = {} as Developer;
// fe.name = 'josh';
// fe.skill = 'TypeScript';
```

<br>

### 하이브리드 타입

```typescript
interface CraftBeer {
  (beer: string): string;
  brand: string;
  brew(): void;
}

function myBeer(): CraftBeer {
  let my: CraftBeer = {
    (beer: string): string {
      return '';
    },
    brand: 'Beer Kitchen',
    brew(): void{}
  };
  return my;
}

let brewedBeer = myBeer();
brewedBeer('My First Beer');
brewedBeer.brand = 'Pangyo Craft';
brewedBeer.brew();
```
