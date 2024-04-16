### 타입스크립트 기본 타입

타입스크립트엔 크게 12개의 타입이 있다.

- Boolean
- Number
- String
- Object
- Array
- Tuple
- Enum
- any
- void
- null
- undefined
- never

<br>

타입 정의는 `:`를 붙여서 사용한다.

```typescript
let str: string = 'hi';
```

<br>

- Array<br>
  배열은 아래와 같이 선언한다.

```typescript
let arr: number[] = [1, 2, 3];
//제네릭을 사용해서 선언하는 경우
let brr: Array<number> = [1, 2, 3];
```

<br>

- Tuple <br>
  튜플은 배열의 길이가 고정되고 각 요소의 타입이 지정되어 있는 타입을 말한다.

```typescript
let arr: [string, number] = ['hi', 10];
```

<br>

- Enum <br>
  이넘은 C, Java와 같은 언어에선 흔히 쓰는 타입으로 특정 값들의 집합을 의미한다.

```typescript
enum Avengers {
  Capt,
  IronMan,
  Thor,
}
let hero: Avengers = Avengers.Capt;
// 인덱스로 접근하는 경우
let hero1: Avengers = Avengers[0];
```

원한다면 이넘의 인덱스를 변경해서 사용할 수 있다.

```typescript
enum Avengers {
  Capt = 2,
  IronMan,
  Thor,
}
let hero: Avengers = Avengers[2]; // Capt
let hero: Avengers = Avengers[4]; // Thor
```

<br>

- any <br>
  말 그대로 모든 타입에 대해서 허용한다는 의미를 갖고 있다.
  그래서 기존 JS로 구현되어 있는 코드에 TS를 점진적으로 적용할 때 활용하면 좋은데 무분별하게 사용하면 TS의 장점을 누릴 수 없다.
  또, 변수에 명확한 타입을 부여하면 vscode에서 해당 타입에 대한 api를 미리보기로 띄워주는데 `any`를 사용하면 그런 거 없다.
  `any`에 대해선 다음에 더 알아보자.

<br>

- void <br>
  반환 값이 없는 함수의 반환 타입이다. `return`이 없거나 있더라도 반환값이 없으면 함수의 반환 타입을 `void`로 지정한다.

```typescript
function printSomething(): void {
  console.log('sth');
}

function returnNothing(): void {
  return;
}
```

<br>

- Never <br>
  함수의 끝에 절대 도달하지 않는다는 의미를 지닌 타입이다.

```typescript
// 이 함수는 절대 함수의 끝까지 실행되지 않는다는 의미
function neverEnd(): never {
  while (true) {}
}
```
