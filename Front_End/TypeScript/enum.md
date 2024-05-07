## Enums

이넘은 특정 값들의 집합을 의미하는 자료형입니다. 타입스크립트에선 문자형 이넘과 숫자형 이넘을 지원합니다.

<br>

### 숫자형 이넘

```typescript
enum Direction {
  Up = 1;
  Down,
  Left,
  Right
}
```

위와 같이 숫자형 이넘을 선언할 때, 초기 값을 주면 차례대로 1씩 증가한다.

```
Up - 1
Down - 2
Left - 3
Right - 4
```

만약 초기 값을 주지 않으면 0부터 차례대로 증가합니다.

```typescript
enum Direction {
  Up, // 0
  Down, // 1
  Left, // 2
  Right, // 3
}
```

### 숫자형 이넘 사용하기

```typescript
enum Response {
  No = 0,
  Yes = 1,
}

function respond(recipient: string, message: Response): void {
  // ...
}

respond('Captain', Response.Yes);
```

※ 숫자형 이넘을 사용할 때 주의할 점은 만약 이넘 값에 다른 이넘 타입의 값을 사용하면 선언하는 이넘의 첫 번째 값에 초기화를 해줘야 한다.

```typescript
enum EnumA {
  A = 1,
  B = 2,
}

enum EnumB {
  X = EnumA.A,
  Y, // 이 부분은 EnumA.A로 초기화됩니다.
}

console.log(EnumB.X); // 출력: 1
console.log(EnumB.Y); // 출력: 2
```

<br>
<br>

### 문자형 이넘

문자형 이넘은 숫자형 이넘과 비슷하지만 런타임에서의 미세한 차이가 있다. <br>

> enum은 런타임시 실제 객체로 존재한다. 왜냐하면 자바스크립트에는 `enum`이 존재하지 않기 때문이다.

일단 문자형 이넘은 이넘 값 전부 다 특정 문자 또는 다른 이넘 값으로 초기화 해줘야 한다.

```typescript
enum Direction {
  Up = 'UP',
  Down = 'DOWN',
  Left = 'LEFT',
  Right = 'RIGHT',
}
```
