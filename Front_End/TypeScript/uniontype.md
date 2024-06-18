## 연산자를 이용한 타입 정의

### Union Type

유니온 타입은 OR같이 A이거나 B이다 라는 타입이다.

```typescript
function logText(text: string | number) {}
```

이렇게 `|`연산자를 사용해서 타입을 여러 개 연결합니다.

- 장점 <br>
  `any`를 사용하는 대신 Union type을 사용하면 타입스크립트의 이점을 살릴 수 있다.

```typescript
function getAge(age: number | string) {
  if (typeof age === 'number') {
    age.toFixed(); // 정상 동작, age의 타입이 `number`로 추론되기 때문에 숫자 관련된 API를 쉽게 자동완성 할 수 있다.
    return age;
  }
  if (typeof age === 'string') {
    return age;
  }
  return new TypeError('age must be number or string');
}
```

<br>

### 주의점

위처럼 단순히 타입이 아닌 인터페이스를 사용한다면 주의해야 할 점이 있다.

```typescript
interface Person {
  name: string;
  age: number;
}

interface Developer {
  name: string;
  skill: string;
}

function introduce(someone: Person | Developer) {
  someone.name; // 정상 동작
  someone.age; // 타입 오류
  someone.skill; // 타입 오류
}
```

왜 오류가 생기냐면 타입스크립트 관점에선 introduce 함수를 실행할 때 Person이 올지 Developer이 나올지 모르기 때문에 오류가 안 나는 방향으로 타입을 추론한다. 그렇기 때문에 함수 안에서 별도의 `타입 가드`를 사용하여 범위를 좁히지 않는 이상 공통적으로 들어있는 속성인 **name**에만 접근이 가능하게 된다.

<br>

---

<br>

### Intersection Type

인터섹션 타입은 여러 타입을 모두 만족하는 하나의 타입을 뜻한다. `&`를 사용한다.

```typescript
interface Person {
  name: string;
  age: number;
}
interface Developer {
  name: string;
  skill: number;
}
type Capt = Person & Developer;
```

이러면 Capt의 타입은 이렇게 된다.

```typescript
{
  name: string;
  age: number;
  skill: number;
}
```
