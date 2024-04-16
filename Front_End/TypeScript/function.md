## 함수

### 함수의 기본적인 타입 선언

```typescript
// javascript
function sum(a, b) {
  return a + b;
}

// typescript
function sum(a: number, b: number): number {
  return a + b;
}
```

기존 자바스크립트 함수의 선언 방식에서 **매개변수**와 **반환 값**에 타입을 추가한다.

<br>

### 함수의 인자

타입스크립트에서는 함수의 인자를 모두 필수 값으로 간주한다. 따라서, 함수의 매개변수를 설정하면 `undefined`나 `null`이라도 인자로 넘겨야 한다.
자바스크립트에선 굳이 꼭 안 써도 괜찮았는데 타입스크립트에선 인자는 모두 써야함

```typescript
function sum(a: number, b: number): number {
  return a + b;
}

sum(10, 20); // 30
sum(10, 20, 30); // error, too many parameters
sum(10); // error, too few parameters
```

만약 자바스크립트처럼 인자를 꼭 넘기지 않고 싶다면 `?`를 사용하면 된다.

```typescript
function sum(a: number, b?: number) {
  return a + b;
}

sum(10, 20); // 30
sum(10, 20, 30); // error, too many parameters
sum(10); // 타입 에러 없음
```

매개변수 초기화는 ES6 문법과 동일하다.

```typescript
function sum(a: number, b = '100'): number {
  return a + b;
}

sum(10, undefined); // 110
sum(10, 20, 30); // error, too many parameters
sum(10); // 110
```

<br>

### REST 문법이 적용된 매개변수

```typescript
function sum(a: number, ...nums: number[]): number {
  const totalOfNums = 0;
  for (let key in nums) {
    totalOfNums += nums[key];
  }
  return a + totalOfNums;
}
```

<br>

### this

타입스크립트에선 `this`가 잘못 사용되었을 때 감지할 수 있다.
`this`가 가리키는 것을 명시하려면 아래와 같이 사용한다.

```typescript
function 함수명(this: 타입) {}
```

<br>
예시를 통해 보자.

<br>

```typescript
interface Vue {
  el: string;
  count: number;
  init(this: Vue): () => {};
}

let vm: Vue = {
  el: '#app',
  count: 10,
  init: function (this: Vue) {
    return () => {
      return this.count;
    };
  },
};

let getCount = vm.init();
let count = getCount();
console.log(count); // 10
```

<br>

### 콜백에서의 this

이번엔 `this`가 콜백으로 전달될 때를 구분해야 하는데 아래와 같이 강제하 수 있다.

```typescript
interface UIElement {
  // 아래 함수의 this:void 코드는 함수의 this타입을 선언할 필요가 없다는 의미다.
  addClickListener(onClick: (this: void, e: Event) => void): void;
}

class Handler {
  info: string;
  onClick(this: Handler, e: Event) {
    // 위의 UIElement인터페이스의 스팩에 this가 필요없다고 했지만 사용했기 때문에 에러가 발생한다.
    this.info = e.message;
  }
}

let handler = new Handler();
uiElement.addClickListener(handler.onClick); //error!
```

만약 `UIElement` 인터페이스의 스펙에 맞춰 `Handler`을 구현하려면 아래와 같다.

```typescript
class Handler {
  info: string;
  onClick(this: void, e: Event) {
    // `this`의 타입이 void이기 때문에 여기서 `this`를 사용할 수 없다.
    console.log('clicked!');
  }
}
let handler = new Handler();
uiElement.addClickListener(handler.onClick);
```

<br>

처음 코드에선 Handler 클래스에 있는 OnClick 메서드에서 this를 사용하려고 하는데 정작 interface에선 addClickListner 메서드의 콜백 함수의 this를 void로 선언해 this를 사용할 수 없는데 사용한다고 해서 오류가 났다.

두 번째 코드는 this를 사용하지 않아서 오류가 나지 않는다.
