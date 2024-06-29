## class

### readonly

클래스 속성에 `readonly`키워드를 사용하면 접근만 가능하게 된다.

```typescript
class Developer {
  readonly name: string;
  constructor(theName: string) {
    this.name = theName;
  }
}
let john = new Developer('John');
john.name = 'John'; // error name is readonly.
```

이처럼 `readonly`를 사용하면 `constructor()`함수에 초기 값 설정 로직을 넣어줘야 하므로 아래와 같이 **인자에** `readonly`를 추가해서 코드를 줄일 수 있다.

```typescript
class Developer {
  readonly name: string;
  constructor(readonly name: string) {}
}
```
